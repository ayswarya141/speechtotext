
# speechtotext
import pyttsx3
#import pyaudio
import speech_recognition as sr
import os
import datetime

name=''
phno=''
r=sr.Recognizer()
c="is it correct?"
def say(command):
    speaker=pyttsx3.init()
    speaker.say(command)
    speaker.runAndWait()

def speak():
    while(1):
        try:
            with sr.Microphone() as source:
                r.adjust_for_ambient_noise(source,duration=0.01)
                audio2=r.listen(source)
                text=r.recognize_google(audio2)
                print(text)
                return text
        except sr.RequestError as e:
                print("cannot identify the voice:{0}".format(e))
        except sr.UnknownValueError:
                return "try again"

while(1):
    q1="tell me your name"
    say(q1)
    name=speak()
    say(c)
    txt=speak()
    if (txt=='yes'):
        break
    else:
        continue

while(1):
    q2="tell me your phone number?"
    say(q2)
    phno=speak()
    say(c)
    txt=speak()
    if (txt=='yes'):
        break
    else:
        continue

y=datetime.datetime.now().strftime("%Y")
m=datetime.datetime.now().strftime("%m")
d=datetime.datetime.now().strftime("%d")
file1=y+"_"+m+"_"+d+".txt"
print(file1)
f=open(file1,'a',encoding="utf-8")
f.write("\n"+name+"\t"+phno)
f.close()
