# Towards a Human-like Open-Domain Chatbot Review

[Paper](https://github.com/vctr7/paper_review/blob/master/Meena(Open-Domain%20Chatbot)/Towards%20a%20Human-like%20Open-Domain%20Chatbot.pdf)

Open-domain chatbot could converse freely in natural language. It can engage in conversation on any topic.

Current open-domain chatbot rely on complex frameworks such as dialog managers with knowledge-based, retrieval-based, rule-based systems. End-to-end neural network approaches offer the simplicity of a single learend model. 

Meena, a generative chatbot model, trained end-to-end on 40 billion words mined and filterd from SNS conversations. The model is trained on multi-turn conversations where the input sequence is all turns of the context and the output sequence is the response.

To measure the performance(quality of Meena), they introduce SSA(Sensibleness and Specificity Average, human evaluation metric). This prevents bots from hiding behind vague replies. 

They compare Meena, humans and other open domain chatbots using the SSA with two types of human evaluation(static and interactive). SSA metric shows strong correlation with Meena’s perplexity. The better that Meena fit its training data, the more sensible and specific its chat reponses became. 

Although their static evaluation dataset is too restricted to capture all aspects of human conversations, Meena acheives such a high SSA score and that there is a correlation between SSA and perplexity means that a human-like chatbot could be in sight if we can attain better perplexity.

Perplexity measures how well the model predicts the test set data; in other words, how accurately it anticipates what people will say next. When interpreting perplexity scores, bear in mind that lower is better and that the theo- retical minimum is one. 


![https://1.bp.blogspot.com/-f_h95j4mpOs/Xi9uCdAZ2WI/AAAAAAAAFOI/RsPCwS1-_KUjE77FzmpX3mGD6BU34y_8wCEwYBhgL/s640/image4.png](https://1.bp.blogspot.com/-f_h95j4mpOs/Xi9uCdAZ2WI/AAAAAAAAFOI/RsPCwS1-_KUjE77FzmpX3mGD6BU34y_8wCEwYBhgL/s640/image4.png)

The best performing Meena model is an Evolved Transformer (ET) (So et al., 2019) seq2seq model with 2.6B parameters, which includes 1 ET encoder block and 13 ET decoder blocks. 
Meena’s hidden size is 2,560 and the number of attention heads is 32. We share the embed- dings across the encoder, the decoder, and the soft- max layer. The encoder and decoder each have a maximum length of 128 tokens (i.e., 256 com- bined). 






![https://1.bp.blogspot.com/-0GSiNr3J1A4/Xi9uB0Zn1hI/AAAAAAAAFOU/zMbsAwsm-mosfgX8pxij2Q1Z_JBZqdV4ACEwYBhgL/s640/image1.png](https://1.bp.blogspot.com/-0GSiNr3J1A4/Xi9uB0Zn1hI/AAAAAAAAFOU/zMbsAwsm-mosfgX8pxij2Q1Z_JBZqdV4ACEwYBhgL/s640/image1.png)


Results indicate most of the variance in the human metrics can be explained by the test perplexity.

[Additional Sample Conversations](https://github.com/google-research/google-research/blob/master/meena/meena.txt)


## Referneces

- [http://ai.googleblog.com/2020/01/towards-conversational-agent-that-can.html](http://ai.googleblog.com/2020/01/towards-conversational-agent-that-can.html)
- [https://blog.pingpong.us/meena-presentation/](https://blog.pingpong.us/meena-presentation/)
