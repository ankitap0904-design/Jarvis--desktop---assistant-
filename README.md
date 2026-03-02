🤖 AI Desktop Voice Assistant – JARVIS



Project Title:
🤖 AI-Based Desktop Voice Assistant (JARVIS)

Developed By:
ankita patel

Technology Used:
Python | AI | Speech Recognition


🟦 Slide 2 — Introduction

JARVIS is an AI-powered desktop voice assistant developed using Python that performs tasks through voice commands.

It helps users interact with computers naturally without using keyboard or mouse.

The system automates daily computer operations using Artificial Intelligence and Voice Recognition.

🟦 Slide 3 — Problem Statement

Traditional computer interaction requires:

Manual typing

Multiple clicks

Time-consuming operations

There is a need for:

✅ Smart automation
✅ Hands-free computer control
✅ Intelligent digital assistant

🟦 Slide 4 — Project Objectives

Develop voice-controlled desktop assistant

Automate daily system tasks

Improve human-computer interaction

Implement AI-based speech recognition

Increase productivity using automation

🟦 Slide 5 — Features of JARVIS

✅ Voice Command Recognition
✅ Text-to-Speech Response
✅ Open Applications Automatically
✅ Google & YouTube Search
✅ Play Music
✅ Tell Time & Date
✅ Wikipedia Information
✅ System Control Commands

🟦 Slide 6 — Technologies Used
Component	Technology
Programming Language	Python
Speech Recognition	SpeechRecognition
Voice Engine	pyttsx3
Automation	OS & Webbrowser
Online Search	Wikipedia API
Media Control	PyWhatKit
🟦 Slide 7 — System Architecture

User Voice Input
⬇
Speech Recognition
⬇
Command Processing
⬇
Task Execution
⬇
Voice Response Output

🟦 Slide 8 — Working Methodology

1️⃣ User gives voice command
2️⃣ Microphone captures audio
3️⃣ Speech converted into text
4️⃣ Command analyzed
5️⃣ Task executed automatically
6️⃣ Assistant responds using voice

🟦 Slide 9 — Project Workflow

Start Program
⬇
Listen Command
⬇
Identify Instruction
⬇
Perform Task
⬇
Speak Response
⬇
Wait for Next Command

🟦 Slide 10 — Sample Commands

"Open Google"

"Open YouTube"

"What is the time?"

"Search Python"

"Play music"

"Open Notepad"

"Exit"

🟦 Slide 11 — Advantages

✅ Hands-free operation
✅ Time saving
✅ Easy accessibility
✅ Smart automation
✅ User-friendly interface

🟦 Slide 12 — Limitations

Requires internet for some commands

Background noise affects recognition

Limited AI understanding

🟦 Slide 13 — Future Enhancements

🚀 GUI Interface
🚀 Face Recognition Login
🚀 Smart Home Integration
🚀 ChatGPT Integration
🚀 Email & WhatsApp Automation
🚀 IoT Device Control

🟦 Slide 14 — Conclusion

JARVIS demonstrates how Artificial Intelligence and Voice Processing can simplify computer usage.

The project provides a foundation for building advanced AI assistants used in modern automation systems
import pyttsx3
import speech_recognition as sr
import datetime
import wikipedia
import webbrowser
import pywhatkit
import os

# Voice Engine
engine = pyttsx3.init()
engine.setProperty('rate', 170)

def speak(text):
    print("Jarvis:", text)
    engine.say(text)
    engine.runAndWait()

def take_command():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        command = r.recognize_google(audio)
        print("You:", command)
        return command.lower()

    except:
        speak("Sorry, say that again")
        return ""

def wish():
    hour = datetime.datetime.now().hour
    if hour < 12:
        speak("Good Morning")
    elif hour < 18:
        speak("Good Afternoon")
    else:
        speak("Good Evening")

    speak("I am Jarvis. How can I help you?")

# Main Program
wish()

while True:
    command = take_command()

    if "time" in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        speak("Current time is " + time)

    elif "open youtube" in command:
        webbrowser.open("https://youtube.com")

    elif "open google" in command:
        webbrowser.open("https://google.com")

    elif "search" in command:
        command = command.replace("search", "")
        speak("Searching...")
        pywhatkit.search(command)

    elif "wikipedia" in command:
        speak("Searching Wikipedia")
        result = wikipedia.summary(command, sentences=2)
        speak(result)

    elif "open notepad" in command:
        os.system("notepad")

    elif "play" in command:
        song = command.replace("play", "")
        speak("Playing " + song)
        pywhatkit.playonyt(song)

    elif "exit" in command or "stop" in command:
        speak("Goodbye")
        break
