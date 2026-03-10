
# Voice AI Mobile Architecture Demo

This repository contains an interactive architecture dashboard demonstrating how a mobile AI voice conversation client works using Flutter and Swift for audio handling.

The goal of this demo is to explain how a production mobile application can support real-time voice conversations with features such as barge-in interruption, persistent microphone state, and low-latency streaming audio communication.

The backend AI infrastructure (Azure OpenAI, Azure Speech Services STT/TTS, and WebSocket orchestration) is assumed to already exist. This demo focuses on the mobile client responsibilities.

---

# Overview

The architecture visualized in this repository explains how a mobile voice assistant handles:

Real-time microphone audio capture  
Streaming PCM audio to a backend over WebSockets  
Speech-to-text processing using Azure Speech Services  
LLM response generation using Azure OpenAI  
Text-to-speech streaming playback  
Voice interruption (barge-in) detection  
Persistent microphone lifecycle management  

The dashboard demonstrates how these components interact in a real conversational AI system.

---

# Key Features Demonstrated

## Barge-In Detection

Users can interrupt the AI while it is speaking.  
Continuous Voice Activity Detection runs even during playback.

When user speech is detected:

Playback stops immediately  
Audio buffers are cleared  
A barge_in WebSocket message is sent to the backend  

Target detection latency is under 150ms.

## Persistent Microphone State

The microphone remains active throughout the entire conversation lifecycle.  
Users do not need to tap the microphone repeatedly between turns.

Conversation flow:

User speaks  
AI responds  
User interrupts or continues speaking  

This produces a natural conversational experience.

---

# System Architecture

The architecture includes the following components.

### Mobile Client

Flutter application layer  
Swift native audio layer  
Voice Activity Detection  
Echo cancellation  

### Communication Layer

WebSocket voice gateway  
Streaming audio transport  

### Backend AI Services

Azure Speech-to-Text  
Azure OpenAI GPT models  
Azure Text-to-Speech  

---

# Audio Pipeline

The audio pipeline implemented in the mobile client follows this sequence.

Microphone capture  
PCM encoding  
WebSocket streaming to backend  
Speech recognition  
LLM response generation  
TTS synthesis  
Jitter buffer for smooth playback  
Audio output to device speaker

This streaming pipeline allows continuous conversational interaction.

---

# Audio Configuration

The client audio configuration matches the backend voice processing pipeline.

### Capture Format

16kHz  
16-bit signed integer  
Mono PCM

### Playback Format

24kHz  
16-bit signed integer  
Mono PCM

### Chunking

100ms audio frames

### Playback Buffer

200ms jitter buffer for smooth streaming playback

---

# UI State Machine

The client uses a deterministic state machine to avoid audio conflicts or stuck states.

States:

Idle  
Listening  
Processing  
Speaking  
Barge-In

State transitions ensure audio sessions remain stable and prevent microphone or playback leaks.

---

# Flutter + Swift Hybrid Design

The mobile application uses a hybrid architecture.

### Flutter Layer

UI and conversation interface  
WebSocket communication  
Conversation state machine  

### Swift Native Layer

Low-latency audio capture using AVAudioEngine  
Audio playback using AudioQueue  
Echo cancellation and audio session control

This approach combines Flutter cross-platform UI with native audio performance.

---

# Performance Targets

The system is optimized for real-time voice conversation.

Target metrics:

Barge-in detection latency below 150ms  
100ms audio streaming chunks  
200ms playback jitter buffer

These parameters ensure conversational responsiveness similar to commercial voice assistants.

---

# Running the Demo

This repository includes a standalone HTML dashboard that explains the architecture visually.

To run the demo locally:

1. Download or clone the repository
2. Open the file:

voice-ai-mobile-architecture.html

The dashboard will open in your browser.

No installation or dependencies are required.

---

# Purpose

This demo was created to demonstrate the architecture of a real-time voice AI mobile client and explain how conversational audio systems can be implemented on mobile platforms.

It focuses on engineering architecture and audio system design rather than UI prototyping.

---

# Author

Kashif Ilyas  
Mobile & Full Stack Engineer
