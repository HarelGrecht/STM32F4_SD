# FPGA Sound Playback System

## Overview

This project enables the playback of sound files stored on an SD card by transmitting data over UART to an FPGA. The system consists of an **STM32F407VGT6** microcontroller and a **Spartan-6 FPGA**. The STM32 reads `.COE` files from the SD card and sends the relevant bytes over UART to the FPGA, which then plays the corresponding sound.

## Features

- Reads **3 different .COE files** from an SD card based on UART input.
- Transmits the sound data to the **Spartan-6 FPGA** over UART.
- The FPGA processes the received data and plays the appropriate sound.

## File Details

The system handles the following `.COE` files:

| Filename    | Description |
|------------|-------------|
| `Cannon.coe` | Plays the Cannon sound |
| `Missle.coe` | Plays the Missile sound |
| `N2.coe` | Plays the N2 sound |

## UART Commands

The system triggers sound playback based on **single-character** UART inputs:

| Input Character | Corresponding Sound |
|----------------|---------------------|
| `C` | **Cannon.coe** |
| `M` | **Missle.coe** |
| `N` | **N2.coe** |

## Hardware Components

- **FPGA:** Spartan-6
- **Microcontroller:** STM32F407VGT6
- **Storage:** SD Card (holds the `.COE` files)
- **Communication:** UART (between STM32 and FPGA)

## System Workflow

1. STM32 waits for a UART command (`C`, `M`, or `N`).
2. Upon receiving a valid input, the STM32:
   - Reads the corresponding `.COE` file from the SD card.
   - Extracts the **read bytes** from the file.
   - Sends the extracted bytes to the **Spartan-6 FPGA** over UART.
3. The FPGA processes the received data and plays the corresponding sound.

## Installation & Setup

### 1. Hardware Setup
- Connect the STM32F407VGT6 to an SD card module.
- Connect the STM32 to the Spartan-6 FPGA via UART.
- Ensure the FPGA is programmed to process incoming UART data and play sounds.

### 2. Software Setup
- Load the `.COE` files onto the SD card.
- Flash the STM32 with the firmware responsible for:
  - Handling UART communication.
  - Reading and sending `.COE` file data.
- Configure the FPGA to receive UART data and play audio.