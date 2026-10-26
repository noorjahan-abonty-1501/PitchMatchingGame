# STM32 Real-Time Pitch-Matching Game

**Embedded Systems | STM32 | Embedded C | Digital Signal Processing**

## Project Overview

This project is an interactive pitch-matching game developed as part of **ECSE 444: Microprocessors at McGill University**.

The system generates a reference audio tone using an STM32 microcontroller, captures the player's attempt to reproduce the tone and estimates the recorded pitch using FFT-based digital signal processing.

The entire signal-processing pipeline runs on the microcontroller, while an interactive UART terminal provides game instructions and feedback.

## Technologies and Tools

- **Microcontroller:** STM32 B-L475E-IOT01A (ARM Cortex-M4)
- **Programming:** Embedded C, ARM assembly optimization
- **Development Environment:** STM32CubeIDE
- **Signal Processing:** CMSIS-DSP, FFT, digital filtering
- **Hardware Peripherals:** DAC, DFSDM microphone, DMA, timers, USART
- **Communication:** UART at 115200 baud
- **System Design:** Finite-state machine

## Key Features

### 1. Audio Tone Generation

- Generates reference tones in the 200–1200 Hz range.
- Uses the STM32 DAC and timer-triggered DMA.
- Outputs a sine waveform through an external speaker.

### 2. Microphone Input and Audio Acquisition

- Captures the player's voice using the onboard DFSDM microphone.
- Uses DMA for microphone sample collection.
- Records approximately 2.5 seconds of audio at around 44.1 kHz.

### 3. FFT-Based Pitch Detection

The embedded DSP pipeline includes:

- DC offset removal
- High-pass filtering
- Hamming windowing
- 1024-point real FFT using CMSIS-DSP
- Spectral peak detection and parabolic interpolation
- Harmonic scoring to estimate the fundamental frequency

The detected pitch is compared with the reference tone to provide player feedback.

### 4. Interactive UART Interface

A terminal-based interface allows the player to:

- Start the game
- Receive gameplay instructions
- Initiate microphone recording
- View the target frequency, detected frequency and accuracy feedback

Interrupt-driven UART reception allows the system to handle input asynchronously.

### 5. Finite-State Machine

The game uses a finite-state machine to coordinate the major operations:

1. MENU
2. PLAY_TONE
3. WAIT_FOR_RECORD
4. RECORD
5. ANALYZE
6. SHOW_RESULTS

This design keeps playback, recording and signal analysis organized into separate stages.

## Performance Optimization

The project included benchmarking and ARM-level UART optimizations.

The final report documented the following improvements during repeated UART operations:

| Operation | Reported Reduction |
|---|---|
| UART transmission benchmark | Approximately 400,000 CPU cycles |
| UART reception callback benchmark | Approximately 150,000 CPU cycles |

These measurements describe the benchmarked communication routines rather than overall game execution time.

## Project Outcome

The completed system integrated audio generation, microphone sampling, onboard frequency estimation and UART-based feedback into an interactive embedded application.

The project demonstrated the use of DMA, peripheral configuration, digital signal processing and state-machine-based control on a resource-constrained microcontroller.

## Team and Acknowledgments

Developed as a collaborative four-member final project for ECSE 444: Microprocessors at McGill University.

Team members:
- Antoine Phan
- Camille Pouliot
- Lena Bousserhane
- Noorjahan Abonty

**My Contributions:** 

## My Contributions

As a member of the four-person development team, I actively contributed to all major stages of the project, from initial system design to final implementation, testing and integration.

My contributions included:

- **System Design and Architecture:** Collaborated on the overall system architecture and finite-state machine to coordinate audio generation, microphone recording, signal processing and user interaction.
- **Embedded Programming and Hardware Configuration:** Contributed to configuring and integrating STM32 peripherals, including the DAC, DFSDM microphone, DMA, timers and UART communication.
- **Digital Signal Processing:** Worked on the FFT-based pitch detection pipeline using CMSIS-DSP, including audio preprocessing, filtering, spectral analysis and frequency estimation.
- **UART Interface and Game Logic:** Helped develop and integrate the interactive terminal interface, user commands, game-state transitions and pitch-matching feedback.
- **Testing and Debugging:** Participated in troubleshooting hardware-software interactions, validating peripheral functionality and testing the integrated system.
- **Performance Evaluation and Documentation:** Contributed to evaluating system performance, reviewing optimization results and documenting the design, implementation and technical outcomes.

Throughout the project, I worked closely with my teammates to integrate individual components into a functioning embedded application, gaining hands-on experience with microcontroller programming, digital signal processing and system-level debugging.

## Original Repository

This repository is a fork of the original collaborative project:

https://github.com/TheGrandMaster1/PitchMatchingGame

The original repository contains the STM32 project source code and configuration files.

## Project Documentation

For more details about the system architecture, hardware implementation, signal processing algorithms and performance evaluation, see the [Final Project Report](docs/ECSE%20444%20-%20Final%20Project%20Final%20Report%20-%20G21.pdf).
