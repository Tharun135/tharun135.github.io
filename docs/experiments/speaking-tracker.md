---
title: Speaking Tracker
description: A high-performance AI speech coach for English fluency practice.
---


An AI-driven mobile application designed to help users bridge the gap between "knowing English" and "speaking English fluently" through immersive, personalized daily practice. Think of it as a personal AI speech coach in your pocket.

!!! tip "Key Tech"
    Built with **React Native (Expo)** and powered by **Google Gemini 1.5 Flash**.

---

## 🧠 The "Brain" (Gemini AI)

The core engine of Speaking Tracker is the integration with **Gemini 1.5 Flash**. Unlike basic language apps, this implementation goes beyond simple text-to-speech:

*   **Audio Analysis**: Converts voice recordings to Base64 and sends them to Gemini for verbatim transcription and a detailed fluency score.
*   **Content Generation**: Dynamically creates "Shadowing" sentences and "Daily Missions" (e.g., *"Use the word 'perspective' 3 times today"*) based on the user's proficiency level.
*   **Roleplay AI**: Acts as a dynamic conversation partner for real-world scenarios like job interviews or ordering coffee.

---

## 🧱 The Core Bricks

### 📱 Dashboard & Roadmap
The **HomeScreen** features a **30-day Roadmap** and a **Streak Tracker**. To make the experience rewarding, it uses `react-native-confetti-cannon` to celebrate daily task completions, boosting user retention through gamification.

### 🎙️ AI Voice Lab
Specialized training modules focused on muscle memory and pronunciation:

*   **Shadowing**: Hear a native-like phrase and repeat it immediately to improve rhythm and intonation.
*   **Tongue Twisters**: Focused muscle-memory training for clarity.
*   **Minimal Pairs**: Distinguishing tricky sounds (e.g., *ship* vs. *sheep*).

### 📓 Voice Journal
Every recording and AI analysis is saved locally using **AsyncStorage**, creating a private, offline-capable digital library of the user's progress from Day 1 to Day 30.

---

## 🛠️ The Tech Stack

| Component | Technology |
| :--- | :--- |
| **Framework** | **React Native** with **Expo** |
| **AI Engine** | **Google Gemini 1.5 Flash** |
| **Audio** | `expo-av` (Recording & Playback) |
| **Speech** | `expo-speech` (Text-to-Speech) |
| **Persistence** | `AsyncStorage` (Local data tracking) |

---

## 📊 Data Foundation

*   **Course Logic (`data/courseData.js`)**: Defines a structured 30-day journey with increasing difficulty and varied topics (Scientific, Argumentative, Reflective).
*   **High-Frequency Chunks (`data/naturalChunks.js`)**: A curated database of phrases that native speakers actually use, which the AI encourages you to incorporate for more natural sounding English.

---

## 🚀 Key Decisions

- **Local-First Data**: All recordings and progress are stored on the device via `AsyncStorage`, ensuring complete privacy and offline accessibility.
- **Dynamic Content**: Instead of static exercises, Gemini generates content on-the-fly, ensuring the app scales with the user's progress.
- **Gamification**: The 30-day roadmap and confetti effects were chosen to solve the biggest problem in language learning: *consistency*.
