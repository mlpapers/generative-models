---
title: "Generative Models"
aliases: ["Generative AI", "Deep generative models"]
tags:
  - generative
  - deep-learning
  - unsupervised
---
# Generative Models

## Overview

- **[Flow matching and diffusion](https://arxiv.org/abs/2506.02070)** — 2025. Derives diffusion and flow matching from stochastic and ordinary differential equations, connecting training objectives, guidance, and image/video architectures. A mathematical overview rather than a new model comparison.

## Latent-variable models

- **[Variational autoencoders](https://arxiv.org/abs/1312.6114)** — 2013. Learns a generative model and an approximate posterior together by optimizing a variational lower bound. Reparameterization enables stochastic gradients through continuous latent samples.
- **[Importance-weighted autoencoders](https://arxiv.org/abs/1509.00519)** — 2015. Uses multiple posterior samples and importance weighting to tighten the VAE likelihood bound. Changes the training objective while retaining a generative network and recognition model.
- **[VQ-VAE](https://arxiv.org/abs/1711.00937)** — 2017. Learns discrete latent codes through vector quantization and fits a learned prior over them. Separates representation learning from modeling the distribution of codes for generation.
- **[VQGAN and latent Transformers](https://arxiv.org/abs/2012.09841)** — 2020. Learns a compact vocabulary of image constituents with a convolutional model, then models their composition with a Transformer. Supports spatial and class conditioning for image synthesis.

## Autoregressive and masked generation

- **[NADE](https://proceedings.mlr.press/v15/larochelle11a.html)** — 2011. Decomposes a joint distribution into tractable neural conditional distributions. Provides normalized probabilities for high-dimensional binary vectors without an intractable partition function.
- **[MADE](https://arxiv.org/abs/1502.03509)** — 2015. Masks network connections so each output depends only on earlier inputs in a chosen ordering. Produces autoregressive conditional probabilities with a feedforward network and supports multiple orderings.
- **[PixelRNN](https://arxiv.org/abs/1601.06759)** — 2016. Models discrete image pixels sequentially using two-dimensional recurrent layers. Assigns probabilities to raw pixel values conditioned on preceding pixels.
- **[Conditional PixelCNN](https://arxiv.org/abs/1606.05328)** — 2016. Uses gated convolutional image-density models conditioned on labels or learned embeddings. Can act as a conditional generator or as an autoregressive decoder within an autoencoder.
- **[WaveNet](https://arxiv.org/abs/1609.03499)** — 2016. Generates raw audio autoregressively, conditioning each sample on earlier waveform values. Additional conditioning supports text-to-speech and speaker-specific synthesis.
- **[MaskGIT](https://arxiv.org/abs/2202.04200)** — 2022. Trains a bidirectional Transformer to predict masked image tokens. Generation fills tokens in parallel and refines them iteratively, replacing fixed raster-order decoding.
- **[Autoregressive generation with diffusion losses](https://arxiv.org/abs/2406.11838)** — 2024. Models continuous token distributions with a diffusion loss inside autoregressive generation, avoiding a discrete vector-quantized tokenizer; includes masked autoregressive image generation.

## Adversarial generation

- **[GANs](https://arxiv.org/abs/1406.2661)** — 2014. Trains a generator against a discriminator that distinguishes generated from observed samples. The idealized minimax analysis assumes unrestricted functions; finite-network training need not reach that solution.
- **[DCGAN](https://arxiv.org/abs/1511.06434)** — 2015. Uses constrained convolutional generator and discriminator architectures for adversarial image generation. Studies learned visual representations and their use in downstream tasks.
- **[Wasserstein GAN](https://arxiv.org/abs/1701.07875)** — 2017. Uses a constrained critic to estimate a Wasserstein objective between generated and observed distributions. The original implementation enforces the critic constraint through weight clipping.
- **[WGAN-GP](https://arxiv.org/abs/1704.00028)** — 2017. Replaces WGAN's weight clipping with a penalty on the critic's input-gradient norm. Addresses optimization problems caused by clipping; it does not establish convergence for every GAN architecture.
- **[Spectral normalization](https://arxiv.org/abs/1802.05957)** — 2018. Normalizes discriminator weights to stabilize adversarial training. Offers a reusable normalization technique instead of changing the generator's latent representation.
- **[StyleGAN](https://arxiv.org/abs/1812.04948)** — 2018. Introduces a style-based generator with control over synthesis at different scales and separate stochastic variation. Studies latent interpolation and separation of visual attributes.
- **[Adaptive discriminator augmentation](https://arxiv.org/abs/2006.06676)** — 2020. Adjusts augmentation during GAN training to counter discriminator overfitting with limited data. Applies to training from scratch and fine-tuning without changing the loss or network architecture.
- **[StyleGAN3](https://arxiv.org/abs/2106.12423)** — 2021. Traces texture sticking to aliasing in the generator and redesigns signal processing to reduce dependence on pixel coordinates. Studies translation- and rotation-equivariant synthesis configurations.

## Invertible density models

- **[NICE](https://arxiv.org/abs/1410.8516)** — 2014. Maps observations invertibly to a factorized latent distribution with tractable inverse and Jacobian determinant. Trains by exact log-likelihood and samples through the inverse transformation.
- **[Real NVP](https://arxiv.org/abs/1605.08803)** — 2016. Uses invertible, non-volume-preserving transformations for tractable density estimation. Supports exact likelihood evaluation and latent inversion under the specified model.
- **[Masked Autoregressive Flow](https://arxiv.org/abs/1705.07057)** — 2017. Stacks autoregressive transformations to increase density-model flexibility. Connects autoregressive density estimation with normalizing flows and generalizes Real NVP.
- **[Glow](https://arxiv.org/abs/1807.03039)** — 2018. Introduces invertible 1×1 convolutions within a normalizing flow. Combines tractable likelihood and latent inversion with parallelizable image synthesis.
- **[Neural spline flows](https://arxiv.org/abs/1906.04032)** — 2019. Uses monotonic rational-quadratic splines as invertible elementwise transforms. Adds flexibility to coupling and autoregressive flows while retaining analytic inversion.
- **[FFJORD](https://arxiv.org/abs/1810.01367)** — 2018. Defines an invertible transformation through an ODE and estimates the Jacobian trace with Hutchinson's estimator. Removes determinant-based architectural restrictions; numerical integration still has a cost.

## Score learning and diffusion

- **[Diffusion probabilistic models](https://arxiv.org/abs/1503.03585)** — 2015. Gradually destroys data structure through a forward diffusion process and learns a reverse process that restores it. Establishes the noising-and-reversal construction for deep generative modeling.
- **[Noise-conditional score networks](https://arxiv.org/abs/1907.05600)** — 2019. Estimates score fields at multiple Gaussian-noise levels and samples through annealed Langevin dynamics. Noise perturbations make score learning practical around low-dimensional data manifolds.
- **[DDPM](https://arxiv.org/abs/2006.11239)** — 2020. Connects diffusion training to denoising score matching through a weighted variational objective. Learns iterative denoising for image generation without adversarial training.
- **[Score-based SDEs](https://arxiv.org/abs/2011.13456)** — 2020. Unifies diffusion and score models through forward and reverse stochastic differential equations. Derives a probability-flow ODE and predictor–corrector sampling procedures.
- **[Improved DDPM](https://arxiv.org/abs/2102.09672)** — 2021. Learns reverse-process variances and modifies diffusion training to improve likelihood and sampling efficiency. Studies likelihood, sample quality, and distribution coverage separately.
- **[Elucidated diffusion models](https://arxiv.org/abs/2206.00364)** — 2022. Separates diffusion design choices in training, network preconditioning, and sampling. Studies how changes can improve both newly trained models and sampling from existing score networks.

## Conditioning and latent architectures

- **[Classifier guidance](https://arxiv.org/abs/2105.05233)** — 2021. Uses gradients from a classifier to steer conditional diffusion sampling. Trades sample diversity against fidelity; the reported image-generation comparisons depend on architecture and guidance settings.
- **[Classifier-free guidance](https://arxiv.org/abs/2207.12598)** — 2022. Combines conditional and unconditional score estimates from joint training. Steers generation without a separate classifier, with a quality–diversity tradeoff controlled at sampling time.
- **[Latent diffusion](https://arxiv.org/abs/2112.10752)** — 2021. Performs diffusion in a pretrained autoencoder's latent space. Cross-attention supports text and other conditioning, while latent compression reduces the dimensionality handled by the denoiser.
- **[Diffusion Transformers](https://arxiv.org/abs/2212.09748)** — 2022. Replaces the U-Net in latent image diffusion with a Transformer operating on latent patches. Studies scaling through network size and token count rather than introducing a new diffusion objective.
- **[Rectified-flow Transformers](https://arxiv.org/abs/2403.03206)** — 2024. Studies training-time sampling for rectified flow and a Transformer with separate image/text weights and bidirectional token interactions. Combines a transport objective with multimodal architecture design.
- **[Diffusion Forcing](https://arxiv.org/abs/2407.01392)** — 2024. Trains a causal sequence model with independent noise levels per token, combining next-token prediction with diffusion denoising so future tokens need not share the past's noise level.

## Flow matching and transport

- **[Flow matching](https://arxiv.org/abs/2210.02747)** — 2022. Trains continuous normalizing flows by regressing vector fields along conditional probability paths, without simulating trajectories during training. Supports diffusion paths and other choices of transport path.
- **[Rectified flow](https://arxiv.org/abs/2209.03003)** — 2022. Fits an ODE to straight interpolations between samples from two distributions. Repeated rectification seeks straighter learned trajectories that can be integrated with fewer steps.
- **[Stochastic interpolants](https://arxiv.org/abs/2209.15571)** — 2022. Constructs a time-dependent density between base and target distributions and learns its velocity with a quadratic objective. Avoids backpropagating through an ODE solver during training.
- **[MeanFlow](https://arxiv.org/abs/2505.13447)** — 2025. Learns average rather than instantaneous flow velocity using an identity linking the two. Targets one-step generation trained from scratch, without requiring a pretrained teacher or distillation.
- **[Diffusion Schrödinger bridges](https://arxiv.org/abs/2106.01357)** — 2021. Uses approximate iterative proportional fitting to learn a stochastic bridge between data and a reference distribution, connecting score-based generation to entropy-regularized transport.

## Sampling and distillation

- **[DDIM](https://arxiv.org/abs/2010.02502)** — 2020. Constructs non-Markovian diffusion processes sharing the DDPM training objective. Changes the sampling procedure to trade computation against sample quality without requiring a new training objective.
- **[DPM-Solver](https://arxiv.org/abs/2206.00927)** — 2022. Analytically handles the linear part of the diffusion ODE and numerically approximates the remaining integral. Provides higher-order sampling without retraining the denoising model.
- **[Progressive distillation](https://arxiv.org/abs/2202.00512)** — 2022. Distills a deterministic diffusion sampler into one using half as many steps, then repeats. Transfers a teacher's sampling behavior into a sequence of progressively shorter samplers.
- **[Consistency models](https://arxiv.org/abs/2303.01469)** — 2023. Learns a direct mapping from noise to data for one-step generation, with optional multistep refinement. Supports both distillation from diffusion models and standalone training.
- **[Latent consistency models](https://arxiv.org/abs/2310.04378)** — 2023. Distills guided latent diffusion into a model predicting probability-flow ODE solutions in latent space. Reduces iterative sampling while retaining conditioning from the pretrained generator.

## Discrete diffusion and flows

- **[D3PM](https://arxiv.org/abs/2107.03006)** — 2021. Extends diffusion to discrete states with structured transition matrices, including absorbing states and embedding-based transitions. Combines a variational bound with an auxiliary cross-entropy objective.
- **[Discrete flow matching](https://arxiv.org/abs/2407.15595)** — 2024. Defines probability paths and sampling rules for discrete variables using learned posterior predictions. Supports non-autoregressive generation without treating tokens as continuous image pixels.
- **[LLaDA](https://arxiv.org/abs/2502.09992)** — 2025. Trains a language diffusion model with forward masking and a Transformer that predicts masked tokens during reverse generation. Uses a likelihood lower bound and supports supervised instruction fine-tuning.

## Energy-based generation

- **[Neural energy-based models](https://arxiv.org/abs/1903.08689)** — 2019. Scales MCMC-based training of neural energy models to images and trajectories. Studies generation, composition, and reconstruction through a learned energy function rather than an explicit feedforward generator.

## Evaluation and memorization

- **[Inception Score](https://arxiv.org/abs/1606.03498)** — 2016. Evaluates generated images through classifier confidence and diversity of predicted classes. Does not compare generated samples directly against a held-out real-image distribution.
- **[Fréchet Inception Distance](https://arxiv.org/abs/1706.08500)** — 2017. Compares Gaussian approximations to real and generated image features using their means and covariances. Measures agreement in the chosen feature space rather than every aspect of the image distribution.
- **[Kernel Inception Distance](https://arxiv.org/abs/1801.01401)** — 2018. Measures squared MMD between Inception features using a polynomial kernel. Its U-statistic estimates this discrepancy without finite-sample bias; the chosen representation and kernel still determine which distributional differences are measured.
- **[Finite-sample FID bias](https://arxiv.org/abs/1911.07023)** — 2019/2020. Chong and Forsyth show that FID bias depends on the evaluated model, so equal sample counts do not remove ranking distortions. They extrapolate toward infinite-sample scores; sample budget and estimator should accompany FID comparisons.
- **[Distribution precision and recall](https://arxiv.org/abs/1806.00035)** — 2018. Separates generated-sample quality from coverage of the target distribution. Exposes distinct failure modes that a single distribution-distance score can combine.
- **[Improved precision and recall](https://arxiv.org/abs/1904.06991)** — 2019. Builds nonparametric representations of real and generated feature manifolds to assess quality and coverage separately. Also studies how truncation changes the generated distribution.
- **[Density and coverage](https://arxiv.org/abs/2002.09797)** — 2020. Revisits failures of precision/recall estimators, including sensitivity to outliers and identical-distribution comparisons. Proposes density and coverage metrics for more informative diagnosis.
- **[Perceptual metric reassessment](https://arxiv.org/abs/2306.04675)** — 2023. Finds weak agreement between common generation metrics and human realism judgments in the studied settings. Examines feature-extractor choice and shows that existing metrics can miss memorization.
- **[Extracting training images](https://arxiv.org/abs/2301.13188)** — 2023. Demonstrates extraction of memorized training examples from studied diffusion models using generation and filtering. Synthetic output is not, by itself, evidence that training records remain private.

## Related Topics

- [Neural Networks](https://mlpapers.org/neural-nets/)
- [Bayesian Inference](https://mlpapers.org/bayesian-inference/)
- [Computer Vision](https://mlpapers.org/computer-vision/)
- [NLP](https://mlpapers.org/nlp/)
