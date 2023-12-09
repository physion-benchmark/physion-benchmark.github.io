---
title: 'Physion V1.5'
description: 'A new release of Physion'
repository_url: 'https://github.com/cogtoolslab/physics-benchmarking-neurips2021'
download_url: 'https://github.com/cogtoolslab/physics-benchmarking-neurips2021#downloading-the-physion-dataset'
layout: default
---
# Physion v1.5

In Physion v1.5, the rendering quality and photorealism have been improved compared to v1. Additionally, v1.5 introduces a new indoor environment, the craft room, adding to the two environments in Physion v1. This version also enhances the diversity of lighting conditions using a collection of 8 unique HDRI skyboxes. These skyboxes are specifically designed to simulate various environmental lighting scenarios, allowing for dynamic time-of-day simulations in the room through adjustments in the orientation of the skyboxes.

## Examples
| Scenario  | Video                                                                                                                             |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------|
| Dominoes  | <video src="static/v15/pilot_dominoes_default_boxroom_0003_img.mp4" controls autoplay loop title="Title" width="200"></video>                 |
| Roll      | <video src="static/v15/pilot_it2_rollingSliding_simple_ramp_box_0029_img.mp4" controls autoplay loop title="Title" width="200"></video>        |
| Collide   | <video src="static/v15/pilot_it2_collision_assorted_targets_tdw_1_dis_1_occ_0014_img.mp4" controls autoplay loop title="Title" width="200"></video> |
| Drop      | <video src="static/v15/pilot_it2_drop_all_bowls_tdw_1_dis_1_occ_0003_img.mp4" controls autoplay loop title="Title" width="200"></video>        |
| Link      | <video src="static/v15/pilot_linking_nl1-8_mg000_aCyl_bCyl_tdwroom1_long_a_0027_img.mp4" controls autoplay loop title="Title" width="200"></video> |
| Support   | <video src="static/v15/pilot_towers_nb4_SJ025_mono1_dis0_occ0_tdwroom_unstable_0027_img.mp4" controls autoplay loop title="Title" width="200"></video> |
| Contain   | <video src="static/v15/pilot-containment-bowl-familiarization_0024_img.mp4" controls autoplay loop title="Title" width="200"></video>         |

## Data Download Links
We provide the data download links below for training the linear probe and evaluation on the test set.

| Scenario   | Readout Train Set                                                                                    | Test Set                                                                                         |
|------------|------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| Dominoes   | [Download Train Set](https://physion-model-readout-set-test.s3.us-east-2.amazonaws.com/dominoes.zip) | [Download Test Set](https://physion-model-test-set-test.s3.us-east-2.amazonaws.com/dominoes.zip) |
| Roll       | [Download Train Set](https://physion-model-readout-set-test.s3.us-east-2.amazonaws.com/roll.zip)     | [Download Test Set](https://physion-model-test-set-test.s3.us-east-2.amazonaws.com/roll.zip)     |
| Collide    | [Download Train Set](https://physion-model-readout-set-test.s3.us-east-2.amazonaws.com/collide.zip)  | [Download Test Set](https://physion-model-test-set-test.s3.us-east-2.amazonaws.com/collide.zip)  |
| Drop       | [Download Train Set](https://physion-model-readout-set-test.s3.us-east-2.amazonaws.com/drop.zip)     | [Download Test Set](https://physion-model-test-set-test.s3.us-east-2.amazonaws.com/drop.zip)     |
| Link       | [Download Train Set](https://physion-model-readout-set-test.s3.us-east-2.amazonaws.com/link.zip)     | [Download Test Set](https://physion-model-test-set-test.s3.us-east-2.amazonaws.com/link.zip)     |
| Support    | [Download Train Set](https://physion-model-readout-set-test.s3.us-east-2.amazonaws.com/support.zip)  | [Download Test Set](https://physion-model-test-set-test.s3.us-east-2.amazonaws.com/support.zip)  |
| Contain    | [Download Train Set](https://physion-model-readout-set-test.s3.us-east-2.amazonaws.com/contain.zip)  | [Download Test Set](https://physion-model-test-set-test.s3.us-east-2.amazonaws.com/contain.zip)  |