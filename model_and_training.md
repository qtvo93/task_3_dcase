# SELDDoANetwork

This is a neural network model designed for Sound Event Localization and Detection (SELD). The architecture combines Convolutional Neural Networks (CNNs) with Transformers and Conformer layers for processing audio data.

## Design Overview

The model consists of two main components: one for Sound Event Detection (SED) and the other for Direction of Arrival (DOA) estimation. It takes a waveform as input, with dimensions `(batch_size, num_channels, data_length)`, where `num_channels` typically represents the number of audio channels, and `data_length` represents the length of the audio data.

The SED and DOA components share the same initial convolutional layers but have separate branches afterward. Each branch involves several layers of convolution followed by average pooling. After the convolutional layers, the data is processed through Conformer layers, which are a variant of Transformer layers designed for sequence modeling tasks in audio and speech processing. Finally, the outputs from both SED and DOA branches are combined using fully connected layers.

## Overall Architecture

- Input: waveform `(batch_size, num_channels, data_length)`
- Output: Combined SED and DOA predictions `(batch_size, n_frames, n_features)`

The architecture comprises the following key components:
- Initial Convolutional Layers
- SED Convolutional Blocks
- DOA Convolutional Blocks
- Conformer Layers for SED and DOA
- Fully Connected Layers for Output Combination

## Layers and Functionality

- **Initial Convolutional Layers:** These layers process the input waveform.
- **SED Convolutional Blocks:** Blocks of convolutional layers followed by average pooling, specifically designed for SED.
- **DOA Convolutional Blocks:** Similar to SED blocks but tailored for DOA estimation.
- **Conformer Layers:** Transformer-based layers specialized for sequence modeling, applied separately for SED and DOA branches.
- **Fully Connected Layers:** Combines the outputs from SED and DOA branches.
- **Activation:** Sigmoid activation is applied to the combined output.

| Layer                    | Design                                                                                                   |
|--------------------------|----------------------------------------------------------------------------------------------------------|
| Initial Convolutional   | Processes the input waveform.                                                                           |
|                          | - Input: 4-channel waveform                                                                            |
|                          | - Output: Feature maps with 16 channels                                                                 |
|                          | - Kernel size: (3, 3)                                                                                  |
|                          | - Pooling: Average pooling with kernel size (2, 2)                                                      |
|                          |                                                                                                          |
| SED Convolutional Blocks| Blocks of convolutions followed by average pooling, tailored for Sound Event Detection (SED).            |
|                          | - Input: 16-channel feature maps                                                                        |
|                          | - Output: Feature maps with 32 channels                                                                 |
|                          | - Kernel size: (3, 3)                                                                                  |
|                          | - Pooling: Average pooling with kernel size (2, 2)                                                      |
|                          |                                                                                                          |
| DOA Convolutional Blocks| Similar to SED blocks but designed for Direction of Arrival (DOA) estimation.                           |
|                          | - Input: 7-channel feature maps (including original 4 channels and appended SED feature maps)           |
|                          | - Output: Feature maps with 32 channels                                                                 |
|                          | - Kernel size: (3, 3)                                                                                  |
|                          | - Pooling: Average pooling with kernel size (2, 2)                                                      |
|                          |                                                                                                          |
| Conformer Layers         | Transformer-based layers specialized for sequence modeling, applied separately for SED and DOA.         |
|                          | - Input: Feature maps with 32 channels                                                                  |
|                          | - Output: Feature maps with 32 channels                                                                 |
|                          | - Depth: 2                                                                                                |
|                          | - Heads: 4                                                                                                |
|                          | - Feedforward multiplier: 4                                                                             |
|                          | - Convolutional expansion factor: 2                                                                     |
|                          | - Convolution kernel size: (31, 1)                                                                      |
|                          | - Attention dropout: 0.2                                                                                 |
|                          | - Feedforward dropout: 0.2                                                                               |
|                          | - Convolution dropout: 0.2                                                                               |
|                          |                                                                                                          |
| Fully Connected Layers   | Combines the outputs from SED and DOA branches.                                                          |
|                          | - Input: Flattened feature maps from both SED and DOA branches                                           |
|                          | - Output: Combined output with appropriate dimensions for final prediction                              |
|                          |                                                                                                          |
| Activation               | Sigmoid activation is applied to the combined output.                                                    |
