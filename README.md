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

- **Flow matching and diffusion** - Derives diffusion and flow matching from stochastic and ordinary differential equations, connecting training objectives, guidance, and image/video architectures. A mathematical overview rather than a new model comparison. [Holderrieth and Erives 2025](<https://arxiv.org/abs/2506.02070> "An Introduction to Flow Matching and Diffusion Models; arXiv").

## Latent-variable models

- **Variational autoencoders** - Learns a generative model and an approximate posterior together by optimizing a variational lower bound. Reparameterization enables stochastic gradients through continuous latent samples. [Kingma and Welling 2014](<https://arxiv.org/abs/1312.6114> "Auto-Encoding Variational Bayes; ICLR").
- **Importance-weighted autoencoders** - Uses multiple posterior samples and importance weighting to tighten the VAE likelihood bound. Changes the training objective while retaining a generative network and recognition model. [Burda et al. 2015](<https://arxiv.org/abs/1509.00519> "Importance Weighted Autoencoders; arXiv").
- **VQ-VAE** - Learns discrete latent codes through vector quantization and fits a learned prior over them. Separates representation learning from modeling the distribution of codes for generation. [van den Oord et al. 2017](<https://arxiv.org/abs/1711.00937> "Neural Discrete Representation Learning; NeurIPS").
- **VQGAN and latent Transformers** - Learns a compact vocabulary of image constituents with a convolutional model, then models their composition with a Transformer. Supports spatial and class conditioning for image synthesis. [Esser et al. 2021](<https://arxiv.org/abs/2012.09841> "Taming Transformers for High-Resolution Image Synthesis; CVPR").

## Autoregressive and masked generation

- **NADE** - Decomposes a joint distribution into tractable neural conditional distributions. Provides normalized probabilities for high-dimensional binary vectors without an intractable partition function. [Larochelle and Murray 2011](<https://proceedings.mlr.press/v15/larochelle11a.html> "The Neural Autoregressive Distribution Estimator; AISTATS").
- **MADE** - Masks network connections so each output depends only on earlier inputs in a chosen ordering. Produces autoregressive conditional probabilities with a feedforward network and supports multiple orderings. [Germain et al. 2015](<https://arxiv.org/abs/1502.03509> "MADE: Masked Autoencoder for Distribution Estimation; ICML").
- **PixelRNN** - Models discrete image pixels sequentially using two-dimensional recurrent layers. Assigns probabilities to raw pixel values conditioned on preceding pixels. [van den Oord et al. 2016](<https://arxiv.org/abs/1601.06759> "Pixel Recurrent Neural Networks; arXiv").
- **Conditional PixelCNN** - Uses gated convolutional image-density models conditioned on labels or learned embeddings. Can act as a conditional generator or as an autoregressive decoder within an autoencoder. [van den Oord et al. 2016](<https://arxiv.org/abs/1606.05328> "Conditional Image Generation with PixelCNN Decoders; NeurIPS").
- **WaveNet** - Generates raw audio autoregressively, conditioning each sample on earlier waveform values. Additional conditioning supports text-to-speech and speaker-specific synthesis. [van den Oord et al. 2016](<https://arxiv.org/abs/1609.03499> "WaveNet: A Generative Model for Raw Audio; arXiv").
- **MaskGIT** - Trains a bidirectional Transformer to predict masked image tokens. Generation fills tokens in parallel and refines them iteratively, replacing fixed raster-order decoding. [Chang et al. 2022](<https://arxiv.org/abs/2202.04200> "MaskGIT: Masked Generative Image Transformer; CVPR").
- **Autoregressive generation with diffusion losses** - Models continuous token distributions with a diffusion loss inside autoregressive generation, avoiding a discrete vector-quantized tokenizer; includes masked autoregressive image generation. [Li et al. 2024](<https://arxiv.org/abs/2406.11838> "Autoregressive Image Generation without Vector Quantization; NeurIPS").

## Adversarial generation

- **GANs** - Trains a generator against a discriminator that distinguishes generated from observed samples. The idealized minimax analysis assumes unrestricted functions; finite-network training need not reach that solution. [Goodfellow et al. 2014](<https://arxiv.org/abs/1406.2661> "Generative Adversarial Networks; arXiv").
- **DCGAN** - Uses constrained convolutional generator and discriminator architectures for adversarial image generation. Studies learned visual representations and their use in downstream tasks. [Radford et al. 2015](<https://arxiv.org/abs/1511.06434> "Unsupervised Representation Learning with Deep Convolutional Generative Adversarial Networks; arXiv").
- **Wasserstein GAN** - Uses a constrained critic to estimate a Wasserstein objective between generated and observed distributions. The original implementation enforces the critic constraint through weight clipping. [Arjovsky et al. 2017](<https://arxiv.org/abs/1701.07875> "Wasserstein GAN; arXiv").
- **WGAN-GP** - Replaces WGAN's weight clipping with a penalty on the critic's input-gradient norm. Addresses optimization problems caused by clipping; it does not establish convergence for every GAN architecture. [Gulrajani et al. 2017](<https://arxiv.org/abs/1704.00028> "Improved Training of Wasserstein GANs; NeurIPS").
- **Spectral normalization** - Normalizes discriminator weights to stabilize adversarial training. Offers a reusable normalization technique instead of changing the generator's latent representation. [Miyato et al. 2018](<https://arxiv.org/abs/1802.05957> "Spectral Normalization for Generative Adversarial Networks; ICLR").
- **StyleGAN** - Introduces a style-based generator with control over synthesis at different scales and separate stochastic variation. Studies latent interpolation and separation of visual attributes. [Karras et al. 2019](<https://arxiv.org/abs/1812.04948> "A Style-Based Generator Architecture for Generative Adversarial Networks; CVPR").
- **Adaptive discriminator augmentation** - Adjusts augmentation during GAN training to counter discriminator overfitting with limited data. Applies to training from scratch and fine-tuning without changing the loss or network architecture. [Karras et al. 2020](<https://arxiv.org/abs/2006.06676> "Training Generative Adversarial Networks with Limited Data; NeurIPS").
- **StyleGAN3** - Traces texture sticking to aliasing in the generator and redesigns signal processing to reduce dependence on pixel coordinates. Studies translation- and rotation-equivariant synthesis configurations. [Karras et al. 2021](<https://arxiv.org/abs/2106.12423> "Alias-Free Generative Adversarial Networks; NeurIPS").

## Invertible density models

- **NICE** - Maps observations invertibly to a factorized latent distribution with tractable inverse and Jacobian determinant. Trains by exact log-likelihood and samples through the inverse transformation. [Dinh et al. 2015](<https://arxiv.org/abs/1410.8516> "NICE: Non-linear Independent Components Estimation; ICLR Workshop").
- **Real NVP** - Uses invertible, non-volume-preserving transformations for tractable density estimation. Supports exact likelihood evaluation and latent inversion under the specified model. [Dinh et al. 2017](<https://arxiv.org/abs/1605.08803> "Density estimation using Real NVP; ICLR").
- **Masked Autoregressive Flow** - Stacks autoregressive transformations to increase density-model flexibility. Connects autoregressive density estimation with normalizing flows and generalizes Real NVP. [Papamakarios et al. 2017](<https://arxiv.org/abs/1705.07057> "Masked Autoregressive Flow for Density Estimation; NeurIPS").
- **Glow** - Introduces invertible 1×1 convolutions within a normalizing flow. Combines tractable likelihood and latent inversion with parallelizable image synthesis. [Kingma and Dhariwal 2018](<https://arxiv.org/abs/1807.03039> "Glow: Generative Flow with Invertible 1x1 Convolutions; NeurIPS").
- **Neural spline flows** - Uses monotonic rational-quadratic splines as invertible elementwise transforms. Adds flexibility to coupling and autoregressive flows while retaining analytic inversion. [Durkan et al. 2019](<https://arxiv.org/abs/1906.04032> "Neural Spline Flows; NeurIPS").
- **FFJORD** - Defines an invertible transformation through an ODE and estimates the Jacobian trace with Hutchinson's estimator. Removes determinant-based architectural restrictions; numerical integration still has a cost. [Grathwohl et al. 2018](<https://arxiv.org/abs/1810.01367> "FFJORD: Free-form Continuous Dynamics for Scalable Reversible Generative Models; arXiv").

## Score learning and diffusion

- **Diffusion probabilistic models** - Gradually destroys data structure through a forward diffusion process and learns a reverse process that restores it. Establishes the noising-and-reversal construction for deep generative modeling. [Sohl-Dickstein et al. 2015](<https://arxiv.org/abs/1503.03585> "Deep Unsupervised Learning using Nonequilibrium Thermodynamics; arXiv").
- **Noise-conditional score networks** - Estimates score fields at multiple Gaussian-noise levels and samples through annealed Langevin dynamics. Noise perturbations make score learning practical around low-dimensional data manifolds. [Song and Ermon 2019](<https://arxiv.org/abs/1907.05600> "Generative Modeling by Estimating Gradients of the Data Distribution; NeurIPS").
- **DDPM** - Connects diffusion training to denoising score matching through a weighted variational objective. Learns iterative denoising for image generation without adversarial training. [Ho et al. 2020](<https://arxiv.org/abs/2006.11239> "Denoising Diffusion Probabilistic Models; NeurIPS").
- **Score-based SDEs** - Unifies diffusion and score models through forward and reverse stochastic differential equations. Derives a probability-flow ODE and predictor-corrector sampling procedures. [Song et al. 2021](<https://arxiv.org/abs/2011.13456> "Score-Based Generative Modeling through Stochastic Differential Equations; ICLR").
- **Improved DDPM** - Learns reverse-process variances and modifies diffusion training to improve likelihood and sampling efficiency. Studies likelihood, sample quality, and distribution coverage separately. [Nichol and Dhariwal 2021](<https://arxiv.org/abs/2102.09672> "Improved Denoising Diffusion Probabilistic Models; arXiv").
- **Elucidated diffusion models** - Separates diffusion design choices in training, network preconditioning, and sampling. Studies how changes can improve both newly trained models and sampling from existing score networks. [Karras et al. 2022](<https://arxiv.org/abs/2206.00364> "Elucidating the Design Space of Diffusion-Based Generative Models; NeurIPS").

## Conditioning and latent architectures

- **Classifier guidance** - Uses gradients from a classifier to steer conditional diffusion sampling. Trades sample diversity against fidelity; the reported image-generation comparisons depend on architecture and guidance settings. [Dhariwal and Nichol 2021](<https://arxiv.org/abs/2105.05233> "Diffusion Models Beat GANs on Image Synthesis; NeurIPS").
- **Classifier-free guidance** - Combines conditional and unconditional score estimates from joint training. Steers generation without a separate classifier, with a quality-diversity tradeoff controlled at sampling time. [Ho and Salimans 2022](<https://arxiv.org/abs/2207.12598> "Classifier-Free Diffusion Guidance; arXiv").
- **Latent diffusion** - Performs diffusion in a pretrained autoencoder's latent space. Cross-attention supports text and other conditioning, while latent compression reduces the dimensionality handled by the denoiser. [Rombach et al. 2022](<https://arxiv.org/abs/2112.10752> "High-Resolution Image Synthesis with Latent Diffusion Models; CVPR").
- **Diffusion Transformers** - Replaces the U-Net in latent image diffusion with a Transformer operating on latent patches. Studies scaling through network size and token count rather than introducing a new diffusion objective. [Peebles and Xie 2023](<https://arxiv.org/abs/2212.09748> "Scalable Diffusion Models with Transformers; ICCV").
- **Rectified-flow Transformers** - Studies training-time sampling for rectified flow and a Transformer with separate image/text weights and bidirectional token interactions. Combines a transport objective with multimodal architecture design. [Esser et al. 2024](<https://arxiv.org/abs/2403.03206> "Scaling Rectified Flow Transformers for High-Resolution Image Synthesis; arXiv").
- **Diffusion Forcing** - Trains a causal sequence model with independent noise levels per token, combining next-token prediction with diffusion denoising so future tokens need not share the past's noise level. [Chen et al. 2024](<https://arxiv.org/abs/2407.01392> "Diffusion Forcing: Next-token Prediction Meets Full-Sequence Diffusion; NeurIPS").

## Flow matching and transport

- **Flow matching** - Trains continuous normalizing flows by regressing vector fields along conditional probability paths, without simulating trajectories during training. Supports diffusion paths and other choices of transport path. [Lipman et al. 2022](<https://arxiv.org/abs/2210.02747> "Flow Matching for Generative Modeling; arXiv").
- **Rectified flow** - Fits an ODE to straight interpolations between samples from two distributions. Repeated rectification seeks straighter learned trajectories that can be integrated with fewer steps. [Liu et al. 2022](<https://arxiv.org/abs/2209.03003> "Flow Straight and Fast: Learning to Generate and Transfer Data with Rectified Flow; arXiv").
- **Stochastic interpolants** - Constructs a time-dependent density between base and target distributions and learns its velocity with a quadratic objective. Avoids backpropagating through an ODE solver during training. [Albergo and Vanden-Eijnden 2023](<https://arxiv.org/abs/2209.15571> "Building Normalizing Flows with Stochastic Interpolants; ICLR").
- **MeanFlow** - Learns average rather than instantaneous flow velocity using an identity linking the two. Targets one-step generation trained from scratch, without requiring a pretrained teacher or distillation. [Geng et al. 2025](<https://arxiv.org/abs/2505.13447> "Mean Flows for One-step Generative Modeling; arXiv").
- **Diffusion Schrödinger bridges** - Uses approximate iterative proportional fitting to learn a stochastic bridge between data and a reference distribution, connecting score-based generation to entropy-regularized transport. [De Bortoli et al. 2021](<https://arxiv.org/abs/2106.01357> "Diffusion Schrödinger Bridge with Applications to Score-Based Generative Modeling; NeurIPS").

## Sampling and distillation

- **DDIM** - Constructs non-Markovian diffusion processes sharing the DDPM training objective. Changes the sampling procedure to trade computation against sample quality without requiring a new training objective. [Song et al. 2021](<https://arxiv.org/abs/2010.02502> "Denoising Diffusion Implicit Models; ICLR").
- **DPM-Solver** - Analytically handles the linear part of the diffusion ODE and numerically approximates the remaining integral. Provides higher-order sampling without retraining the denoising model. [Lu et al. 2022](<https://arxiv.org/abs/2206.00927> "DPM-Solver: A Fast ODE Solver for Diffusion Probabilistic Model Sampling in Around 10 Steps; NeurIPS").
- **Progressive distillation** - Distills a deterministic diffusion sampler into one using half as many steps, then repeats. Transfers a teacher's sampling behavior into a sequence of progressively shorter samplers. [Salimans and Ho 2022](<https://arxiv.org/abs/2202.00512> "Progressive Distillation for Fast Sampling of Diffusion Models; ICLR").
- **Consistency models** - Learns a direct mapping from noise to data for one-step generation, with optional multistep refinement. Supports both distillation from diffusion models and standalone training. [Song et al. 2023](<https://arxiv.org/abs/2303.01469> "Consistency Models; ICML").
- **Latent consistency models** - Distills guided latent diffusion into a model predicting probability-flow ODE solutions in latent space. Reduces iterative sampling while retaining conditioning from the pretrained generator. [Luo et al. 2023](<https://arxiv.org/abs/2310.04378> "Latent Consistency Models: Synthesizing High-Resolution Images with Few-Step Inference; arXiv").

## Discrete diffusion and flows

- **D3PM** - Extends diffusion to discrete states with structured transition matrices, including absorbing states and embedding-based transitions. Combines a variational bound with an auxiliary cross-entropy objective. [Austin et al. 2021](<https://arxiv.org/abs/2107.03006> "Structured Denoising Diffusion Models in Discrete State-Spaces; NeurIPS").
- **Discrete flow matching** - Defines probability paths and sampling rules for discrete variables using learned posterior predictions. Supports non-autoregressive generation without treating tokens as continuous image pixels. [Gat et al. 2024](<https://arxiv.org/abs/2407.15595> "Discrete Flow Matching; NeurIPS").
- **LLaDA** - Trains a language diffusion model with forward masking and a Transformer that predicts masked tokens during reverse generation. Uses a likelihood lower bound and supports supervised instruction fine-tuning. [Nie et al. 2025](<https://arxiv.org/abs/2502.09992> "Large Language Diffusion Models; arXiv").

## Energy-based generation

- **Neural energy-based models** - Scales MCMC-based training of neural energy models to images and trajectories. Studies generation, composition, and reconstruction through a learned energy function rather than an explicit feedforward generator. [Du and Mordatch 2019](<https://arxiv.org/abs/1903.08689> "Implicit Generation and Generalization in Energy-Based Models; arXiv").

## Evaluation and memorization

- **Inception Score** - Evaluates generated images through classifier confidence and diversity of predicted classes. Does not compare generated samples directly against a held-out real-image distribution. [Salimans et al. 2016](<https://arxiv.org/abs/1606.03498> "Improved Techniques for Training GANs; NeurIPS").
- **Fréchet Inception Distance** - Compares Gaussian approximations to real and generated image features using their means and covariances. Measures agreement in the chosen feature space rather than every aspect of the image distribution. [Heusel et al. 2017](<https://arxiv.org/abs/1706.08500> "GANs Trained by a Two Time-Scale Update Rule Converge to a Local Nash Equilibrium; NeurIPS").
- **Kernel Inception Distance** - Measures squared MMD between Inception features using a polynomial kernel. Its U-statistic estimates this discrepancy without finite-sample bias; the chosen representation and kernel still determine which distributional differences are measured. [Bińkowski et al. 2018](<https://arxiv.org/abs/1801.01401> "Demystifying MMD GANs; ICLR").
- **Finite-sample FID bias** - Chong and Forsyth show that FID bias depends on the evaluated model, so equal sample counts do not remove ranking distortions. They extrapolate toward infinite-sample scores; sample budget and estimator should accompany FID comparisons. [Chong and Forsyth 2020](<https://arxiv.org/abs/1911.07023> "Effectively Unbiased FID and Inception Score and where to find them; CVPR").
- **Distribution precision and recall** - Separates generated-sample quality from coverage of the target distribution. Exposes distinct failure modes that a single distribution-distance score can combine. [Sajjadi et al. 2018](<https://arxiv.org/abs/1806.00035> "Assessing Generative Models via Precision and Recall; NeurIPS").
- **Improved precision and recall** - Builds nonparametric representations of real and generated feature manifolds to assess quality and coverage separately. Also studies how truncation changes the generated distribution. [Kynkäänniemi et al. 2019](<https://arxiv.org/abs/1904.06991> "Improved Precision and Recall Metric for Assessing Generative Models; NeurIPS").
- **Density and coverage** - Revisits failures of precision/recall estimators, including sensitivity to outliers and identical-distribution comparisons. Proposes density and coverage metrics for more informative diagnosis. [Naeem et al. 2020](<https://arxiv.org/abs/2002.09797> "Reliable Fidelity and Diversity Metrics for Generative Models; ICML").
- **Perceptual metric reassessment** - Finds weak agreement between common generation metrics and human realism judgments in the studied settings. Examines feature-extractor choice and shows that existing metrics can miss memorization. [Stein et al. 2023](<https://arxiv.org/abs/2306.04675> "Exposing flaws of generative model evaluation metrics and their unfair treatment of diffusion models; NeurIPS").
- **Extracting training images** - Demonstrates extraction of memorized training examples from studied diffusion models using generation and filtering. Synthetic output is not, by itself, evidence that training records remain private. [Carlini et al. 2023](<https://arxiv.org/abs/2301.13188> "Extracting Training Data from Diffusion Models; arXiv").

## Related topics

- [Neural Networks](https://mlpapers.org/neural-nets/)
- [Bayesian Inference](https://mlpapers.org/bayesian-inference/)
- [Computer Vision](https://mlpapers.org/computer-vision/)
- [NLP](https://mlpapers.org/nlp/)
