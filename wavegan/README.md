# WaveGAN Review

[Paper](https://github.com/vctr7/paper_review/blob/master/wavegan/wavegan.pdf)

Audio signals are sampled at high temporal resolutions, and learning to synthesize audio requires capturing structure across a range of timescales.
a first attempt at applying GANs to unsupervised synthesis of raw-waveform audio. 

Synthesizing audio is practical application in creative sound design for music and film.

Unsupervised strategy for mapping low-dimensional latent vectors to high-dimensional data. 

Advantage 
  
  1. useful for data augmentation in data hungry speech recognition system. 
  
  2. enable rapid and straight forward sampling of large amounts of audio. 


WaveGAN : Flatten the DCGAN architecture to operate in one dimension, resulting in a model with the same number of parameters and numerical operations as its two-dimensional analog. 

[GAN](https://en.wikipedia.org/wiki/Generative_adversarial_network) : Discriminator is trained to determine if an example is real of fake, and Generator is trained to fool the discriminator into thinking its output is real.

![https://miro.medium.com/max/1292/1*XiAXk60ur-NeZm2c49s7nA.png](https://miro.medium.com/max/1292/1*XiAXk60ur-NeZm2c49s7nA.png)

This equation is to minimizing the [Jensen-Shannon divergence](https://en.wikipedia.org/wiki/Jensen%E2%80%93Shannon_divergence). But original GANs are difficult to train and prone to failure cases. 

So, use [Wasserstein-1](https://en.wikipedia.org/wiki/Wasserstein_metric) distance between generated and data distribution  To minimize Wasserstein distance, they suggenst a GAN training algorithm. Discriminator is trained as a function that assists in computing the Wasserstein distance. 

Or use weight clipping by [1-Lipshitz](https://en.wikipedia.org/wiki/Lipschitz_continuity). 

Or use gradient penalty to replace the above methods.

![https://media.arxiv-vanity.com/render-output/2406730/x1.png](https://media.arxiv-vanity.com/render-output/2406730/x1.png)

Periodic patterns are unusual in natural images but a fundamental structure in audio. 
DCGAN uses small, 2d filters while WaveGAN uses longer, 1d filters and a larger upsampling factor. 
As a consequence, correlations across large windows are commonplace in audio. 16 kHz, a 440 Hz sinusoid takes over 36 samples to complete a single cycle. This suggensts that filters with larger receptive fields are needed to process large audio. 

DCGAN, popularized usage of GANs for image synthesis. 
DCGAN Generator uses the transposed convolution operation to iteratively upsample low-resolution feature mpas into a high-resolution image. 
To widened an receptive field, use longer 1d filters of length 25 instead of 5x5. Modify Discriminator in a simliar way, using length 2d to 1d, and increasing stride from 2 to 4. 
These changes result in WAVEGAN having the same number of parameters, numerical operations and output dimnesionality as DCGAN.

64x64 pixels equivalent to 4096 audio samples, add one additional layer to the model resulting in 16384 samples, slightly more than one second of audio at 16kHz.

Phase Shuffling : Generative image models that upsampled by CNN are known to produce checkerboard artifacts in images. Periodic patterns are less common in images, and thus the Discriminator can learn to reject images that contain them. 
For audio, similar artifacts are perceived as pitched noise when may overlap with frequencies commonplace in the real data, making the Discriminator's objective more challengin.
However, the artifact frequencies will always occur at a particular phase, allowing the Discriminator to learn a trivial policy to reject generated examples. This may inhibit the overall optimization problem.

![https://storage.googleapis.com/groundai-web-prod/media/users/user_14/project_38663/images/x6.png](https://storage.googleapis.com/groundai-web-prod/media/users/user_14/project_38663/images/x6.png)

To prevent the problem which the Discriminator from learning such a solution, need 'phase shuffle' operations with hyperparameter n.
Phase shuffle randomly perturbs the phase of each layer's activations by put to the next layer. Apply this method only to Discriminator, as the latent vector already provides the Generator a mechanism to manipulate the phase of a resultant waveform.
It helps the Discriminator's work by requiring invariance to the phase of the input waveform.



