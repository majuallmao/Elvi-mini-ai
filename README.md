elvi_core.py - Elvi Mini Main AI Core

import os import openai import datetime import pyttsx3 import speech_recognition as sr import webbrowser from langchain.llms import OpenAI from langchain.chains import ConversationChain from langchain.memory import ConversationBufferMemory

=== INIT ===

openai.api_key = os.getenv("OPENAI_API_KEY") engine = pyttsx3.init() memory = ConversationBufferMemory() llm = OpenAI(temperature=0.7) conversation = ConversationChain(llm=llm, memory=memory)

=== SPEAK FUNCTION ===

def speak(text): print(f"Elvi: {text}") engine.say(text) engine.runAndWait()

=== LISTEN FUNCTION ===

def listen(): r = sr.Recognizer() with sr.Microphone() as source: print("Listening...") audio = r.listen(source) try: query = r.recognize_google(audio) print(f"You said: {query}") return query except Exception as e: print("Sorry, I didn't get that.") return ""

=== MAIN COMMAND EXECUTOR ===

def run_elvi(): speak("Hello! I am Elvi Mini, your supreme AI.") while True: query = listen().lower()

if "exit" in query or "bye" in query:
        speak("Goodbye! Talk to you soon.")
        break

    elif "open youtube" in query:
        webbrowser.open("https://youtube.com")
        speak("Opening YouTube.")

    elif "what's the time" in query or "time" in query:
        now = datetime.datetime.now().strftime("%H:%M:%S")
        speak(f"Current time is {now}.")

    elif query.strip() != "":
        response = conversation.predict(input=query)
        speak(response)

=== RUN ELVI MINI ===

if name == "main": run_elvi()
