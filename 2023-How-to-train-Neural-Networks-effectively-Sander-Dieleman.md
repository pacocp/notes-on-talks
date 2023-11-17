# How to train Neural Networks effectively
## Sander Dieleman

**2023 Mediterranean Machine Learning Summer School**

[Link to the talk](https://www.youtube.com/watch?v=wO4quYlQUyE)

---

- Most ideas don’t work
- Think deeply about the metric that you are going to use.
- The metric is something different to the loss function!
- Iteration speed is key. At the beginning start with something small and iterate fast. Then scale the model!
- Optimize the number of experiments that you can run.
- Resources are limited. So better to estimate if something is going to help or not, and then revisit based on the results you have obtained.
- You need to invest in engineering! Use hardware efficiently. Use a profiler. Look at performance vs wall-clock time.
- Matrix multiplications are fast! Use them.
- Two models on hyperparameter optimisation: optimising an objective and building understanding.
- When sweeping hyperparameters, grid search can be useful to build understanding.
- Random Search can give you a good understanting since good values are taken more ofter.
- Residual connections work really well.
- Normalisation is key. Normalisation can go before or after linear operations.
- Batchnorm is falling out of favour, since it is a bug magnet. You will always need to include the update state.
- In the context of Transformers, FlashAttention is gaining momentum and it is cool.
- QK Normalisation also works really well in Transformers (including vision transformers).
- Transformers doesn’t have topological biases, so you can induce them with embeddings. Pretty cool for instance for gene expression.
- Vector quantization can works really well for encoding information in a bottleneck layer.
- You can use different components in the loss function to enforce certain constraints.
- You should start and use Adam.
- Tuning beta2 is important, since it is related with the moment.
- Learning rate schedulers, use them! Warmup works really well for transformers. It is crucial, specially when you are scaling the models. At the beginning you want to have a high learning rate to explore the space, and then use a small one to reach a good solution.
- Exponential moving average works really well for generative models! This comes at a significant memory cost.
- What kind of parallelism you want to do? Usually data parallelism for up to billion of parameters, then you need to use model parallelism.
- As a rule of thumb, minimise communication across devices.
- Training in half-precision! Helps with memory. However, it introduces numerical instability.
- You can train the model and then perform quantisation to reduce the model size. However, this introduces outliers (since weights and activations have a long tail).
- Distillation is really cool for training a smaller model.
