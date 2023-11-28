# CVPR - Denoising diffusion models

- Two proceses: forward diffusion process add noise to input, reduce the noise backward
- We add noise based on a normal distribution in T steps.
- It has a very simple mean and standard deviation, that we are scaling by a value (beta).
- We can define a joint distribution for all the conditions.
- We can generate an image at a given step based on the initial state.
- With the diffusion kernel.
- For sampling we can use the reparametrization trick:
  $x_t = \sqrt{\alpha_t}X_0 + \sqrt{(1-\alpha_t)} \epsilon$ where $e ~ N(0, I)$
- The $\beta_t$ values are very important.
- The forward process is similar to a Gaussian convolution
- We don't have access to the PDF of the real distribution, thus we don't have access to the intermediate distribution either
- We can go back at the end of the forward process and sample from the denoising distribution.
- We can approximate it using a normal distribution if $\beta_t$ is small in each diffusion step.
- We have $p(x_T) = N(X_T;0,I)$. And by using the parameters $\theta$ we can approximate it using a trainable network $p_{\theta}(X_{t-1}|x_t) = N(x_{t-1}; \mu_{\theta}(x_t,t), \alpha_{t}{^2} I)$
- This will predict the average version of that noisy image.
- We can use it to define the joint distrubtion of all trajectories: $p_{\theta}(x_{0:T}) = p(x_T) \prod_{t=1}^{T} p_\theta(x_{t-1}|x_{t})$
- This is the product of the conditionals
- We can form variational upper bound that is commonly used for training variational autoencoders.
- If you assume that the mean is modeled as a scaling of the network we can use it to obtain an easier mathematical objective
- So basically we train a network to predict the noise that was used in the image
- Algorithm for the training:
  1. repeat
  2. $x_0 ~ q(x_0)$
  3. $t ~$ Uniform$({1, ..., T})$
  4. $\epsilon ~ N(0, I)$
  5. Take gradient descent step on: $\nabla_{\theta} || \epsilon - \epsilon_{\theta}(\sqrt{\alpha_t}x_0 + \sqrt{1 - \alpha_t} \epsilon t) ||^2$
  6. until converged
- Algorithm for sampling:
  1. $x_T ~ N(0, I)$
  2. for t = T,...1, do
  3. $z ~ N(0, I)$
  4. $x_{t-1} = \frac{1}{\sqrt{\alpha_t}} (x_t - \frac{1-\alpha_t}{\sqrt{1-\alpha_t}} \epsilon_\theta (x_t,t)) + \sigma_t z$
  5. end for
  6. return $x_0$
- This is a deterministic mapping
- Oridinary Differential Equations you don't have access to the functions but you know how they evolve over time. 
- You can solve the ODE, so we can find xt that are a linear approximation.
- Stochastic SDifferential Equation, we also have a stochastic componenbt that adds noise. You can solve them similarly to ODE. But you have an additional term that you sampke from a gaussian distribution and you scale it using a diffusion coefficient. You have different random walks.
- Song et al. showed that the forward process can be distritizate using a Stochastic Differential Equation (SDE). 
- Forward diffusion SDE: $dx_t = - \frac{1}{2} \beta(t) x_t dt + \sqrt{\beta(t)) dw_t}$ Here we have the drift term (pull towards mode) and the diffusion term (injects noise)
- The drift term always towards the center, and the diffusion term is a dispersion so you know at the end you get a normal distribution. This is a continious version of the process.
- We just need to undo this process to generate. You have the score function, that is the logarithmic derivative the data as time t: $\nabla_{x_t} \log_{q_t}(x_t)$

