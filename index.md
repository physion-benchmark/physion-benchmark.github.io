---
title: 'Physion: Evaluating Physical Prediction from Vision in Humans and Machines'
description: 'Daniel M. Bear*, Elias Wang*, Damian Mrowca*, Felix Binder*, Hsiao-Yu Fish Tung, R.T. Pramod, Cameron Holdaway, Sirui Tao, Kevin Smith, Fan-Yun Sun, Li Fei-Fei, Nancy Kanwisher, Jushua B. Tenenbaum, Daniel L.K. Yamins**, and Judith Fan**'
repository_url: 'https://github.com/cogtoolslab/physics-benchmarking-neurips2021'
paper_url: 'https://datasets-benchmarks-proceedings.neurips.cc/paper/2021/file/d09bf41544a3365a46c9077ebb5e35c3-Paper-round1.pdf'
publication_venue: 'NeurIPS 2021'
layout: default
---
<div class="video-container">
  <iframe class="video" src="static/scenario_animation.mp4" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
</div>

Almost all of our behavior is guided by _intuitive physics_: our implicit knowledge of how different objects and materials behave in a wide variety of common scenarios. We know to stack boxes from largest to smallest, to place a cup on its flat base rather than its curved side, and to hook a coat on a hanger lest it fall to the floor. As AI algorithms begin to play larger roles in our daily lives, we must ensure that they, too, can make safe and effective decisions. But do they understand the physical world well enough to do so?

### [](#header-3)Probing physical understanding in machines
To answer this question, we need a way of “asking” an AI model how it perceives a physical scenario. Two approaches have been popular in prior work: (1) training models to answer questions about simple synthetic scenarios, such as [whether a stack of toy blocks will fall over](https://openaccess.thecvf.com/content_ECCV_2018/papers/Oliver_Groth_ShapeStacks_Learning_Vision-Based_ECCV_2018_paper.pdf) or an object will [emerge from behind an occluder](https://intphys.com/index.html); and (2) training and testing large neural networks on the task of video synthesis, i.e. asking them to [https://arxiv.org/pdf/1802.07687.pdf](predict the upcoming frames of a movie).

Each of these approaches, despite some appeal, has severe drawbacks. The former dovetails with research in cognitive science, which has found that people can make accurate predictions about key physical events, like the tower falling, while abstracting away low-level details. To date, however, this sort of benchmarking in AI has been restricted to a small number of highly simplified scenarios that fail to capture the variety and complexity of everyday physics.

The latter strategy of video synthesis, on the other hand, makes few assumptions about how an algorithm should understand physical scenarios, allowing large neural networks to be trained and tested on real, unlabeled visual data. For this reason, video synthesis is a popular training task in robotics: if an agent can make accurate predictions about how its environment will change based on the actions it takes, then it should be able to accomplish its goals. But predicting everything about how a scene will change is enormously hard, even with gargantuan datasets. As a result, these models appear to succeed only when restricted to a particular, narrow domain. Moreover, humans would fail at video synthesis; it is therefore unlikely to measure the intuitive physics that allows us to generalize our knowledge and achieve our goals in new, wide-ranging settings. 

### [](#header-3)Physion: a diverse and challenging benchmark for visual intuitive physics 
To fill the large gap between these approaches, we need a way to test for human-like physical understanding in diverse, challenging, and visually realistic environments. We therefore introduce the Physion Dataset and Benchmark. Our key contributions are
* Training and testing sets for eight realistically simulated and rendered 3D scenarios that probe different aspects of physical understanding: how objects roll, slide, fall, and collide; how one object may support, contain, or attach to another; and how multiple objects made of different materials interact.
* A unified testing procedure for comparing AI models to humans on a challenging prediction task, which depends on grasping the physical phenomena in the Physion dataset.
* An initial evaluation of state-of-the-art computer vision and graph neural network models on the Physion benchmark, which suggests that today’s algorithms will need to incorporate more physically explicit, object-centric visual scene representations to reach human-like ability.

#### [](#header-4)Creating a diverse and challenging benchmark 
On a visually and physically narrow benchmark, many state-of-the-art models could overfit and achieve “super-human performance” without understanding everyday physics in the generalizable, flexible way that people do. On the other hand, a benchmark that relies too much on higher level knowledge, such as asking what will happen next in YouTube videos, would not test intuitive physical understanding. We therefore took an intermediate approach: the Physion scenarios focus on specific (but partly overlapping) physical phenomena that occur often in everyday life. Stimuli for each scenario were physically simulated and visually rendered using the highly realistic, Unity3D-based ThreeDWorld environment, which adeptly handles diverse physics like projectile object motion and collisions, rolling and sliding, and even multi-material interactions. We provide training and testing sets of 2000 and 150 movies, respectively, for each scenario, as well as code for generating additional training data.

#### [](#header-4)Directly comparing humans to machines at physical understanding 
To measure how well both models and people understand each scenario, we created a common readout task for all stimuli: Object Contact Prediction. This task has a person or model observe the first 1.5 seconds of each Physion movie, then make a binary prediction about whether two of the objects in the scene -- indicated by their red and yellow appearance -- will come into contact during the remaining, unseen portion of the movie. People easily grasp this task and make accurate predictions, even when the stimuli are challenging (see below.) To measure model behavior, we adapt standard methods of transfer learning to our prediction task: models pretrained on unlabeled Physion data, other datasets (like ImageNet), or both, are fit with a linear readout of their learned features to make binary predictions about upcoming object contact. Since models and humans make predictions for the same task on the same stimuli, we can directly compare their behavior as a function of (a) model architecture, (b) pretraining task, and (c) which subsets of learned features are used to make the object contact prediction.

### [](#header-3)How do today’s AI algorithms measure up to humans? 
Humans make very accurate predictions about the Physion stimuli, but they aren’t perfect: across 100 participants per scenario, average performance on the prediction task was ~75%. Some scenarios appeared to be more challenging than others: for instance, people had a harder time judging the effects of object-object attachment in the Link scenario than how objects would move down a ramp or across the floor in the Roll scenario. Moreover, some stimuli in each scenario appeared to be “physically adversarial”: most people predicted one outcome, but in the ground truth movie the opposite occurred -- often due to a physical fluke, like an object teetering on the brink of falling over. Imperfect human accuracy on Physion is a feature, not a bug: it means that a (hypothetical) super-human model might be overfitting or picking up on cues that people don’t use to make physical predictions. Since abstracting away low-level detail is an important part of how we make general, fast, and efficient judgments, it is important to know whether current and future AI models do the same.

For the time being, however, state-of-the-art in computer vision appears to be far behind humans at making physical predictions: none of the vision neural networks we tested, whether they were trained on video synthesis or supervised tasks, used an object-centric or structureless scene representation, or had a convolutional or transformer-based encoder architecture, came close to human performance on any of the eight Physion scenarios. 

#### [](#header-4)What’s missing from computer vision models for physical understanding? 
Fortunately, closing this large gap between models and machines is not a total shot in the dark: we were able to find cases where neural networks can perform as well as people. Algorithms called Graph Neural Networks (GNNs) made predictions on some of the Physion scenarios as accurately as humans, suggesting that they may hold some of the keys to intuitive physical understanding. However, these models were given an enormous advantage over the human participants: instead of receiving visual input (i.e., movies), they operate on the ground truth physical state of the ThreeDWorld simulator. This means that they have near-perfect knowledge of each object’s boundaries, 3D shape, and fine-scale trajectory; are unhindered by occlusion or only seeing the front surfaces of objects; and are explicitly told which parts of the scene can be ignored or compressed into a more efficient representation. 

Thus, these models bypass the amazing computations our brain uses to parse a scene as a set of physical objects moving through 3D space. The GNNs’ success suggests, though, that if we understood these computations -- that is, if we could implement a visual encoding model that produced object-centric, physically explicit scene representations like the ones the GNNs use -- then we might obtain algorithms with human-like physical understanding. Such vision models are therefore an attractive target for future work and for using Physion to bring AI more in line with human intuitive physics.


This is how to include a video:

<div class="video-container">
  <iframe class="video" src="https://www.youtube.com/embed/ZoNP1gwMsU8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
</div>

Text can be **bold**, _italic_, or ~~strikethrough~~.

[Link to another page](another-page).

There should be whitespace between paragraphs.

There should be whitespace between paragraphs. We recommend including a README, or a file with information about your project.

# [](#header-1)Header 1

This is a normal paragraph following a header. GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.

## [](#header-2)Header 2

> This is a blockquote following a header.
>
> When something is important enough, you do it even if the odds are not in your favor.

### [](#header-3)Header 3

```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```

```ruby
# Ruby code with syntax highlighting
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

#### [](#header-4)Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### [](#header-5)Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### [](#header-6)Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![](https://assets-cdn.github.com/images/icons/emoji/octocat.png)

### Large image

![](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
