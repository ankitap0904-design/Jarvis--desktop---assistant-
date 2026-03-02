
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
