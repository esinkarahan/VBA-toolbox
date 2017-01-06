---
title: "Bayesian learning"
---
* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

Bayesian decision theory (BDT) is a probabilistic framework that is concerned with how decisions are made or should be made, in ambiguous or uncertain situations. The “normative” approach to BDT focuses on identifying the “optimal” or “rational” decision in a given context. This has been applied extensively to methods supporting decisions (e.g., statistical testing). In contradistinction, “descriptive” BDT attempts to describe what people actually do. In this context, optimal decisions are considered as quantitative predictions that can be tested against observed behaviour.

BDT relies on two processes: belief updating and decision making, which are related to the key elements of BDT; namely, prior distributions and utility functions, respectively. In the context of perceptual categorisation, prior beliefs are motivated by the inherent ambiguity of sensory information, which leads to uncertainty about the underlying causes of sensory signals. Priors effectively resolve this ambiguity and are thought to be the basis of most sensory illusions and multistable perceptual effects. In addition, BDT is bound to a perspective on preferences, namely “utility theory”, which was explored in length in the context of economic decisions. In this context, utility functions can be regarded as a surrogate for a task goal or, equivalently, a scoring of the subject’s preferences.

Bayesian models can be used either to capture peoples' hidden priors beliefs (which shape the way they learn) and/or preferences (which map beliefs onto actions). Typically, they are used to model choices and/or reaction times. Many Bayesian learning models are available in the VBA toolbox. We refer interested readers to [Daunizeau et al. (2010a)](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0015554) for details regarding the specificity of inverting BDT models. 


## A cue-outcome associative learning model for reaction times

The script `demo_AVL_recog.m` demonstrates a simple Bayesian learning model, which predicts trial-by-trial variations in reaction times during an associative learning task. This script reprocudes the simulations of the companion paper [Daunizeau et al. (2010b)](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0015555). 

The model was designed to provide a normative way of solving participants' task, which we briefly describe here. At each trial, people were asked to categorize a visual outcome (face or house) as quickly as possible. Just prior to the visual stimulus presentation, they were exposed to an auditory cue (high-pitch or low-pitch tone) that was predictive of the visual outcome. Participants had to learn this association, which was changing over the course of the experiment.

The constituents of the BDT model are:

- a set of hierarchically organized states (3 per available action). The first hierarchical level captures potential perceptual uncertainty regarding visual outcomes. The second hierarchical level contains the moments (mean and variance: 2 states) of peoples' posterior belief about the cue-outcome contingency.
- two evolution parameters that control the perceptual uncertainty and the prior variance of cue-action contingency, respectively.
- two observation parameters that control the speed-accuracy trade-off during perceptual categorization.

The Bayesian learning rule consists in an trial-by-trial update of the cue-outcome contingency, which essentially approximates a [Kalman filter](https://en.wikipedia.org/wiki/Kalman_filter). 


## Associative learning in the context of volatile environments



A volatile environment undergoes frequent and unpredictable changes in behaviourally-relevant contingencies. Critically, an optimal agent should adapt her learning rate to the environmental volatility, which may itself change over time. This implies that an optimal Bayesian learner should also track the environmental volatility. In [Mathys et al. (2011)](http://www.frontiersin.org/human_neuroscience/10.3389/fnhum.2011.00039/abstract), we proposed a simple Bayesian learning rule that possesses this form of adaptive fitness. The script `demo_volatileVB.m` demonstrates this (hierarchical) Bayesian learning model in the context of an associative learning task. 

The constituents of this model are:

- a set of hierarchically organized states (6 per available action). The first two levels are similar to the above model (3 states). The third level contains the moments (mean and variance: 2 states) of peoples' posterior belief about the the action-outcome contingency's volatility. 
- three evolution parameters that control the dynamical changes of the agent's effective learning rate (volatility weight, base volatility, and volatility transition prior variance).
- two observation parameters: bias and temmperature.


The script `demo_dynLearningRate.m` demonstrates how one can use inversion diagnostics (e.g., [Volterra kernels]({{ site.baseurl }}/wiki/Volterra-decomposition.md)) to detect systematic changes in learning rates that conform to volatile Bayesian learning. In turn, these diagnostics can be used to gradually increase the complexity of learning models to capture the sophistication of (hidden) computational mechanisms.