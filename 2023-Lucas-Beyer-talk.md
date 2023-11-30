# Lucas Beyer talk

- You need to scale both models and data at the same time, at least in vision.
- And also it is shown that large models are really good at few-show learning.
- Over the last few years Language is becoming the API of vision.
- Pretrain on large-scale data with image-text pairs and with that way of pretraining, we have a model that can write down and it can tell you if it is there or not.
- They found it works really well with sigmoid loss instead of softmax loss for the CLIP model.
- Then, once you have learned the model we can do 0shot transfer.
- You get the similarity score, and then the higher the score the better the text describe the image
- By doing so you don't need to know the task as priori.
- Still, zero shot classification is still far behind in comparison to supervised models.
- Extensively exploiting prompting didn't really affect much the performance of the model at least for CLIP.
- You can use LiT, that use any vision encoder that you want already trained, you freeze it, and then you just train the text encoder. 
- This gives a good text capability to any model that you like.
- The pre-trained image model can serve as a bridge across languages, anchoring concepts
- This would help to create multilingual models, similarly to how a multilingual children might learn
- Meta made something similar as LiT with ImageBind
- All communities are trying to tokenize your data and use it with a transformer, and it looks like it works!
- Tokenize depends on your modality. But basically is explitting your data into chunks that serve as input for your transformer
- The main problem is that it cannot have really long sequence length
- This is very easy with transformers but it much harder with other networks
- Autoregressive models can be really cool for image-text tasks!

