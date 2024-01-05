** Week 1 (Dec 18-24): Understanding the Problem and Dataset

*** Complete a detailed review of the challenge description and dataset.

The dataset included multichannel recordings from two sites with spatial and temporal annotations for target sound classes. Compared to the previous version, STARSS23 added 4 hours of material, 360° video recordings, and distance labels for annotated sound events.

Evaluation Metrics:

Evaluation is based on metrics that jointly assess localization and detection performance, including F1-score, error rate, localization error, and localization recall.
Metrics are computed in one-second non-overlapping frames.


Challenge Tracks:

Participants can choose between two tracks: audio-only and audiovisual.
Audio-only track focuses on SELD labels with multichannel audio input.
Audiovisual track incorporates 360° video recordings during both training and evaluation.


*** Begin developing a basic understanding of the provided sample data.

Recording Setup:

The recordings are made in two different sites: Tampere, Finland, by the Audio Research Group (ARG) of Tampere University, and in Tokyo, Japan, by Sony.
Each recording clip is part of a session in a unique room, with varying participants, sound-making props, and scene scenarios.
The scenes are loosely scripted to provide good variability in the data, considering factors like presence, density, movement, and spatial distribution of sound events.
Target Classes:
The dataset includes annotations for 13 target sound event classes, loosely following the Audioset ontology. Some examples of classes include female speech, male speech, clapping, telephone, laughter, domestic sounds, footsteps, door open/close, music, musical instrument, water tap, bell, and knock.

Recording Formats:
The dataset provides recordings in two spatial formats:

First-Order Ambisonics (FOA): Converted from a 32-channel microphone array using encoding filters.
Tetrahedral Microphone Array (MIC): Four microphones positioned in spherical coordinates, with an analytical expression for the directional array response.

Video Data:

The dataset includes simultaneous 360° video recordings aligned with the audio recordings.
Video data is made available with participants' consent, and faces are blurred for privacy.

Additional Information:

Annotations include temporal and spatial information for prominent events of target classes, captured by an optical tracking system.
Some classes have subclasses or detailed descriptions to aid participants in understanding the content, such as types of telephone sounds or musical instruments.
There are occasional localized sound events not annotated and considered as interferers, like computer keyboard, shuffling cards, dishes, pots, and pans.
Natural background noise, like HVAC noise, is present in recordings at varying levels.

Dataset Specifications:

Recordings from 16 unique rooms (4 in Tokyo, 12 in Tampere) for the development set.
Training and evaluation sets include recordings from both sites, with additional material in Tampere.
Audio recordings have a sampling rate of 24kHz and 16-bit depth.
Video recordings have a resolution of 1920x960 and a frame rate of 29.97 fps.

*** Read from the previous year’s work to see what other researchers did for preprocessing.

No. 1 Team

THE NERC-SLIP SYSTEM FOR SOUND EVENT LOCALIZATION AND DETECTION OF DCASE2023 CHALLENGE

In the audio-only SELD task, they apply the audio channel swapping (ACS) technique for data augmentation. A ResNet-Conformer architecture is used as the acoustic model. To handle overlapping mixtures, they introduce a class-dependent sound separation (SS) model and fuse its features with SELD predictions for specific event classes.

For audio-only inference, they perform data augmentation using ACS, simulate multi-channel data, and generate sound event clips for separation model training. The SS-SELD method involves training SS models for specific classes, using them as a front-end for extracting class-specific sounds and improving SELD detection. The network training involves FOA format data, log-mel spectra features, and ACS for augmentation.

Model ensemble strategies, including activity-coupled Cartesian DOA (ACCDOA) and multi-ACCDOA fusion, are employed to improve generalization. Post-processing involves dynamic thresholding and fusion of SS-SELD and SELD predictions.

The paper demonstrates successful results on the STARSS23 development dataset, showcasing improvements over baseline systems for both audio-only and audio-visual SELD tasks. The authors effectively utilize data augmentation, sound separation, model ensemble, and post-processing strategies to enhance performance.


No. 2 Team

ATTENTION MECHANISM NETWORK AND DATA AUGMENTATION FOR SOUND EVENT LOCALIZATION AND DETECTION

First, they generated additional spatial audio files for training by using Audioset, FSD50k, and TAU Spatial Room Impulse Responses Database (TAU-SRIR DB). They addressed the issue of dataset imbalance between real and simulated data by keeping half of the training data from the real dataset and half from the simulated dataset during training. For data augmentation, they applied techniques such as random cutout, time-frequency masking, frequency shifting, and augmix.

Their model architecture, called Model 1, utilized a Resnet-Conformer network with a multi-scale channel attention mechanism (MS-CAM) for improved feature extraction. They also introduced attentive statistics pooling to enhance feature discriminability. Additionally, they incorporated the EINV2 framework with multi-ACCDOA output, aiming to efficiently detect overlapping problems of events.

In terms of input features, they used audio files in First Order Ambisonics (FOA) format, extracting 4-channel log-mel spectrograms and 3-channel sound intensity vectors, combined into a 7-channel feature.

For training, they employed the Adam optimizer, a batch size of 256, and trained the model for 100 epochs. They used a learning rate schedule and addressed the imbalance between real and synthetic datasets by selecting half of the datasets from each for every training round.

The proposed system demonstrated significant improvement over the baseline on the development dataset of DCASE2023 Task 3, as indicated by performance metrics such as location-dependent error rate (ER≤20°), location-dependent F-score (F≤20°), class-dependent localization error (LECD), and localization recall (LRCD). Model 1 and Model 2 individually outperformed the baseline, and their ensemble (Ensemble 1) achieved even better results, demonstrating the effectiveness of their approach.

No.3 Team

A DATA GENERATION METHOD FOR SOUND EVENT LOCALIZATION AND DETECTION IN REAL SPATIAL SOUND SCENES

Data Synthesis: The authors simulate multi-channel spatial recordings by convolving monophonic sound event samples from FSD50K and AudioSet with multi-channel spatial room impulse responses (SRIRs). This addresses the scarcity of real-scene recordings.

SRIRs: The SRIRs are sourced from the TAU Spatial Room Impulse Response Database (TAU-SRIR DB) and are also computationally generated using the image source method (ISM).
Data Augmentation Chains: The authors leverage previously proposed data augmentation chains, combining operations like Mixup, Random Crop, SpecAugment, and frequency shifting. These augmentation strategies aim to enhance the model's ability to handle diverse sound event scenarios.

Model: The authors use the Event-Independent Network V2 (EINV2) with a track-wise output format. EINV2 consists of two branches for sound event detection and direction-of-arrival (DoA) estimation. It employs a Conv-Conformer architecture, and tracks are used to predict sound events with corresponding DoA.

Training:
Data Cleaning: PANNs are utilized to clean sound event examples selected from FSD50K and AudioSet.
Training Data: Additional datasets are used to supplement the limited real-scene data. Simulated data is generated using the DCASE provided generator code.
Evaluation: The proposed method is evaluated on the dev-test set of STARSS23, outperforming the baseline on the Sony-TAU Realistic Spatial Soundscapes 2023 dataset.

Results:
The proposed solution significantly outperforms the baseline method on the dev-test set, demonstrating the effectiveness of the data generation method and augmentation chains.
In summary, the authors tackle the challenge of limited real-scene data by combining real and simulated datasets. The use of data synthesis, SRIRs, data augmentation, and the EINV2 model collectively contribute to the success of the proposed method in sound event localization and detection in real spatial sound scenes.
