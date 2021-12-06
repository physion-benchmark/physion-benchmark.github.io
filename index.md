---
title: 'Physion: Evaluating Physical Prediction from Vision in Humans and Machines'
description: 'Daniel M. Bear*, Elias Wang*, Damian Mrowca*, Felix Binder*, Hsiao-Yu Fish Tung, R.T. Pramod, Cameron Holdaway, Sirui Tao, Kevin Smith, Fan-Yun Sun, Li Fei-Fei, Nancy Kanwisher, Joshua B. Tenenbaum, Daniel L.K. Yamins**, and Judith Fan**'
repository_url: 'https://github.com/cogtoolslab/physics-benchmarking-neurips2021'
paper_url: 'https://datasets-benchmarks-proceedings.neurips.cc/paper/2021/hash/d09bf41544a3365a46c9077ebb5e35c3-Abstract-round1.html'
publication_venue: 'NeurIPS 2021'
download_url: 'https://physics-benchmarking-neurips2021-dataset.s3.amazonaws.com/Physion.zip'
layout: default
---

# Do today's vision models understand everyday physical phenomena as well as people do?

**_Physion_ is a dataset and benchmark for evaluating AI models against human intuitions about how objects move and interact with one another. We test a broad suite of state-of-the-art models and a large number of people on the same 1.2K examples of objects rolling, sliding, falling, colliding, deforming, and more. We show that humans surpass current computer vision models at predicting how scenes unfold. Our experiments suggest that endowing these models with more physically explicit scene representations is a promising path toward human-like physical scene understanding, and thus safer and more effective AI.** 

### Watch our talk at NeurIPS 2021

<p style="overflow:hidden; padding-bottom:56.25%; position:relative; height:0">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/Jz7ImDazcJI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="left:0; top:0; height:100%; width:100%; position:absolute"></iframe>
</p>

<hr>

# Probing physical understanding in machines

Almost all of our behavior is guided by _intuitive physics_: our implicit knowledge of how different objects and materials behave in a wide variety of common scenarios. We know to stack boxes from largest to smallest, to place a cup on its flat base rather than its curved side, and to hook a coat on a hanger, lest it fall to the floor. As AI algorithms play a larger role in our daily life, we must ensure that they, too, can make safe and effective decisions. But do they understand the physical world well enough to do so?

To answer this, we need a way of “asking” an AI model how it perceives a physical scenario. Two approaches have been popular in prior work: (1) asking models questions about simple scenarios, such as whether [a block tower will fall](https://openaccess.thecvf.com/content_ECCV_2018/papers/Oliver_Groth_ShapeStacks_Learning_Vision-Based_ECCV_2018_paper.pdf) or an object will [emerge from behind an occluder](https://intphys.com/index.html); and (2) training and testing large neural networks on _video synthesis_, i.e. asking them to [predict the upcoming frames of a movie](https://arxiv.org/pdf/1802.07687.pdf).

Each of these approaches has merits and drawbacks. The first dovetails with research in cognitive science, which has found that people make [accurate predictions about key physical events](https://www.pnas.org/content/110/45/18327.short), like the tower falling, while abstracting away low-level details. To date, however, this sort of benchmarking in AI has been restricted to a few simple scenarios that lack the variety and complexity of everyday physics.

The second approach makes few assumptions about _how_ an algorithm should understand scenes. For this reason, video synthesis on real, unlabeled data is a popular training task in robotics: if an agent can make accurate predictions about its environment, it might accomplish its goals. But predicting everything about how a scene changes is enormously hard, [even with gargantuan datasets](https://arxiv.org/abs/2106.13195). As a result, these models currently succeed only in narrow domains. Moreover, humans do not even [_see_](https://en.wikipedia.org/wiki/Inattentional_blindness) everything that happens in a movie, let alone predict it; video synthesis is therefore unlikely to capture the intuitions we use to make decisions in new, wide-ranging settings. 

<p>
    <video loop autoplay muted controls style="width:100%; height:auto">
        <source src="static/scenario_animation.mp4" type="video/mp4">
    </video>
</p>

# Physion: a benchmark for visual intuitive physics

To fill the large gap between these approaches, we need a way to test for _human-like_ physical understanding in _diverse, challenging, and visually realistic environments_. We therefore introduce the **Physion Dataset and Benchmark**. Our key contributions are:
* Training and testing sets for _**eight realistically simulated and rendered 3D scenarios**_ that probe different aspects of physical understanding: how objects roll, slide, fall, and collide; how one object may support, contain, or attach to another; and how multiple objects made of different materials interact,
* A _**unified testing protocol**_ for comparing AI models to humans on a challenging prediction task,
* An initial _**evaluation of state-of-the-art computer vision and graph neural network models**_ on the Physion benchmark, the results of which suggest that today’s algorithms should incorporate more physically explicit scene representations to reach human ability.


## Using [ThreeDWorld](https://www.threedworld.org/) to design the benchmark

On a narrow benchmark, models might overfit and achieve “super-human performance” without understanding everyday physics in the general, flexible way people do. On the other hand, a benchmark that relied on higher level "semantic" knowledge would not directly test intuitive physics. We therefore took an intermediate approach to designing Physion: each of its eight scenarios focuses on specific physical phenomena that occur often in everyday life. Stimuli for each scenario were physically simulated and visually rendered using the Unity3D-based [ThreeDWorld environment](https://www.threedworld.org/), which adeptly handles diverse physics like projectile motion and object collisions, rolling and sliding across surfaces of varying friction, and clothlike or deformable material interactions. We provide training and testing sets of 2000 and 150 movies, respectively, for each scenario, as well as code for generating more training data.

<p align="center">
    <img src="static/comparison_table.png" />
</p>


## Comparing humans and machines


To measure how well both models and people understand each scenario, we created a common readout task for all stimuli: _Object Contact Prediction_. This task has a person or model observe the first portion of each Physion movie, then make a prediction about whether two of the scene's objects will come into contact during the remaining, unseen portion. People easily grasp this task and make accurate predictions. To measure model behavior, we adapted the standard method of _transfer learning_ to our prediction task: models pretrained on unlabeled Physion movies or other datasets are probed with a linear readout to make predictions about upcoming object contact. Since models and humans do the same task on the same stimuli, we can directly compare their behavior.

<p align="center">
    <img src="static/human_model_comparison.png" />
</p>


# How do today’s AI models compare to humans? 


Humans make accurate predictions about the Physion stimuli, but they aren’t perfect. Some scenarios were more challenging than others: for instance, people had a harder time judging the effects of object-object attachment in the **Link** scenario than how objects would fall down a ramp in the **Roll** scenario. Moreover, some stimuli appeared to be “physically adversarial”: most people predicted one outcome, but in the ground truth movie the opposite occurred -- often due to a physical fluke, like an object teetering on the brink of falling over. Imperfect human performance is a feature of our approach, not a bug: it means that a (hypothetical) super-human model might be overfitting to scenario-specific cues that people ignore. Since abstracting away low-level detail is key to how we make general and efficient judgments, it is crucial to know whether current and future AI models do the same.

For the time being, though, the state-of-the-art in computer vision appears far behind humans at making physical predictions: _none of the vision neural networks we tested_, regardless of model architecture or pretraining task, came close to human performance on the Physion benchmark. While the models that received object-related training signals fared slightly better than those that didn't, control experiments suggested that these models often fail to make human-like judgments about what they _observe_, even before making predictions. Thus, current vision models appear to lack essential components of human intuitive physics.

<p align="center">
    <img src="static/model_pipeline.png" />
</p>


# )What’s missing from vision algorithms to achieve physical understanding? 

Fortunately, the way to close this large gap between models and machines isn't a total shot in the dark: in some cases neural networks _did_ perform as well as people. Models called Graph Neural Networks (GNNs) reached human accuracy on some Physion scenarios, suggesting that they may hold aspects of intuitive physical understanding. However, these models have an enormous advantage over people: instead of receiving visual input, they operate on the _ground truth physical state_ of the ThreeDWorld simulator. This means that they have near-perfect knowledge of each object’s boundaries, 3D shape, and fine-scale trajectory; are unhindered by occlusion; and are explicitly told which parts of the scene can be ignored or compressed into a more efficient representation. 


Thus, these models bypass the amazing computations our brain uses to parse a scene as a set of [physical objects moving through 3D space](https://onlinelibrary.wiley.com/doi/pdf/10.1207/s15516709cog1401_3#:~:text=Object%20perception%20does%20accord%20with,each%20other%20only%20on%20contact) -- computations that emerge, without direct supervision, [by the end of human infancy](https://pubmed.ncbi.nlm.nih.gov/10349761/). The GNNs’ success suggests, though, that if we understood these computations -- that is, if we could implement visual encoding models that produce object-centric, physically explicit scene representations like the ones the GNNs use -- then we might obtain algorithms with (more) human-like physical understanding. Such vision models are therefore an attractive target for future work and for using Physion to bring AI in line with human intuitive physics.

<p align="center">
    <img src="static/results_summary.png" />
</p>