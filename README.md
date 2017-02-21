# Voice-Recognition-Workshop @ CodeDayNJ Winter 2017
## Python Modules Needed (Using Python v 2.7)
1. Requests [Installation Guide] (http://docs.python-requests.org/en/master/user/install/)
2. Pyaudio [Installation Guide] (https://people.csail.mit.edu/hubert/pyaudio/)

## Instructions
### Bluemix
1. Make an account [here] (https://console.ng.bluemix.net/)
2. On the left-hand menu under services, scroll down to 'Watson' and select 'Speech to Text'
3. Rename your service name and credentials if you like and select 'Create'

### Code To Communicate With IBM STT
1. Write code to record audio and save it to a wav file. If need be, copy the file in this repo
2. Incorporate the following code:
```
import requests
USERNAME = '<Username>'
PASSWORD = '<Password>'

url = 'https://stream.watsonplatform.net/speech-to-text/api/v1/recognize'

headers={'Content-Type': 'audio/wav'}

audio = open('file.wav', 'rb')

r = requests.post(url, data=audio, headers=headers, auth=(USERNAME, PASSWORD))

text_file = open("WatsonSTTResult.txt", "w")
text_file.write(r.text)
text_file.close()
```
### Code to Retrieve Transcript from File
```
f = open('WatsonSTTResult.txt', 'r')

while True:
  text = f.readline()
  confidence = ''
  transcript = ''
  num = 0
  if '"confidence": ' in text:
    confidence = text[29:(len(text) - 3)]
    num = float(confidence)
    f.readline()
    if (num > 0.85):
      transcript = text[30:(len(text) - 3)]
   elif f.readline() == '':
		break
```
