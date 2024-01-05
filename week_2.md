
## Week 2 (Dec 25-31): Data Preprocessing and Exploration

*** Implement data loading and preprocessing scripts for both FOA and MIC formats. *** 

Done using Baseline system provided batch data loading script

*** Investigate and/or Visualize audio data for initial insights. ***

Done using `cls_feature_class.py` in function get_mel_spectrogram

*** Read from previous year works to see what others did for training and advanced set up. ***

### Paper 1 

**Advancements:**
- Utilized an ensemble method combining multiple models for sound event localization and detection.
- Introduced a trajectory-based fusion approach to improve system performance.
- Employed self-supervised learning on unlabeled data for better generalization.

**News:**
- Leveraged self-supervised learning for sound event detection, showcasing a novel approach to exploit unlabeled data effectively.
- Introduced trajectory-based fusion as an innovative strategy for enhancing the overall system's localization and detection capabilities.

---

### Paper 2 

**Advancements:**
- Addressed the weakly supervised scenario where only audio tags are available for training.
- Utilized a two-stage pipeline involving audio tagging followed by event localization and detection.
- Incorporated self-attention mechanisms to capture long-range dependencies in the audio signals.

**News:**
- Innovatively tackled weakly supervised learning for sound event localization, catering to scenarios with limited annotated data.
- The two-stage pipeline presented a structured approach, separating audio tagging and localization tasks, potentially offering a more effective learning process.

---

### Paper 3 

**Advancements:**
- Developed a data generation method for sound event localization and detection in real spatial sound scenes.
- Simulated multi-channel spatial recordings by convolving sound event examples with multi-channel spatial room impulse responses (SRIRs).
- Integrated data augmentation chains, combining various augmentation operations.

**News:**
- Addressed the challenge of limited real-scene recordings by proposing a comprehensive data generation method.
- Introduced the use of SRIRs for simulating spatial recordings, enhancing the model's ability to handle real-world spatial sound scenarios.
- Highlighted the effectiveness of data augmentation chains, emphasizing their role in training models to handle diverse sound event scenarios.
