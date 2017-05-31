# PythonSnippets
Just a page with python snippets

```
▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄ 
          ▀█▄▀▄▀██████ ▀█▄▀▄▀████▀ 
            ▀█▄█▄███▀   ▀██▄█▄█
```
## Simple post request
[Python request guide](http://docs.python-requests.org/en/master/)

[Stack overflow with source of code](http://stackoverflow.com/questions/4476373/simple-url-get-post-function-in-python)

```python
import requests

# request url
url = "http://httpbin.org/post"

# post data
payload = {'key1': 'value1', 'key2': 'value2'}

# POST with form-encoded data
r = requests.post(url, data=payload)

# Response, status etc
print(r.status_code, r.reason)
print(r.text)
```

## link + port is up check

```python
def check(ip, port):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.settimeout(2)
    try:
        s.connect((ip, port))
        print str(ip) + " - Port " + str(port) + " reachable"
    except socket.error as e:
        print str(ip) + " - Error on connect for port " + str(port)
    s.close()
```

## Get battery percentage in windows
```python
from ctypes import *

class PowerClass(Structure):
    _fields_ = [('ACLineStatus', c_byte),
            ('BatteryFlag', c_byte),
            ('BatteryLifePercent', c_byte),
            ('Reserved1',c_byte),
            ('BatteryLifeTime',c_ulong),
            ('BatteryFullLifeTime',c_ulong)]    

powerclass = PowerClass()
result = windll.kernel32.GetSystemPowerStatus(byref(powerclass))

print powerclass.BatteryLifePercent
```

## Base64/SHA512
```python
import base64

text = "something something"

encoded = base64.b64encode(text)
decoded = base64.b64decode(encoded)
```

```python
import hashlib
print hashlib.sha512("TEXT TO HASH").hexdigest()
```

## Raspberry Pi GPIO (just some of my old code)
```python
# External module imports
import RPi.GPIO as GPIO
import time

# Pin Definitons:
pinC    = 4    # P7
pinB    = 25   # P6
pinRed  = 24   # P5
pinA    = 23   # P4

# Pin Setup:
GPIO.setmode(GPIO.BCM) # Broadcom pin-numbering scheme
GPIO.setup(pinA, GPIO.OUT) # LED pin set as output
GPIO.setup(pinB, GPIO.OUT) # LED pin set as output
GPIO.setup(pinC, GPIO.OUT) # LED pin set as output
GPIO.setup(pinRed, GPIO.OUT) # LED pin set as output

# Initial state for LEDs:

GPIO.output(pinA, GPIO.HIGH)
GPIO.output(pinB, GPIO.HIGH)
GPIO.output(pinC, GPIO.HIGH)
GPIO.output(pinRed, GPIO.HIGH)

time.sleep(5)

GPIO.output(pinA, GPIO.LOW)
GPIO.output(pinB, GPIO.LOW)
GPIO.output(pinC, GPIO.LOW)
GPIO.output(pinRed, GPIO.LOW)

print("Here we go! Press CTRL+C to exit")
try:
    while True:
        time.sleep(1)
        GPIO.output(pinA, GPIO.HIGH)
        time.sleep(1)
        GPIO.output(pinB, GPIO.HIGH)
        time.sleep(1)
        GPIO.output(pinC, GPIO.HIGH)
        time.sleep(1)
        GPIO.output(pinA, GPIO.LOW)
        GPIO.output(pinB, GPIO.LOW)
        GPIO.output(pinC, GPIO.LOW)
        GPIO.output(pinRed, GPIO.HIGH)
        time.sleep(1)
        GPIO.output(pinRed, GPIO.LOW)

except KeyboardInterrupt: # If CTRL+C is pressed, exit cleanly:
    GPIO.cleanup() # cleanup all GPIO

```

## Basic barchart in Matplotlib

```python
import matplotlib.pyplot as plt
import numpy as np

# data = [] | labels = []
def make_chart(data, labels, ylabel='', title=''):
    #data -> data for each bar
    N = len(data)  # amount of bars

    ind = np.arange(N)  # the x locations for the bars
    width = 0.6         # the width of the bars

    # prepare diagram
    fig, ax = plt.subplots()
    bar1 = ax.bar(ind, data, width, color='r')

    # x labels
    ax.set_xticks(ind)  # label location
    ax.set_xticklabels(labels, rotation='vertical')  # label for each bit of data

    # more labels
    ax.set_ylabel(ylabel)
    ax.set_title(title)

    # open graph window
    plt.show()
```

## Manipulate clipboard
```python
from Tkinter import Tk
r = Tk()
r.withdraw()                # Prevent window from opening
txt = r.clipboard_get()     # Get current clipboard string
r.clipboard_clear()         # Clear clipboard
r.clipboard_append("hello") # Add text to clipboard
r.update()                  # Save clipboard data (else it disapears after r.destroy())
r.destroy()
```

## Easygui
```python
import easygui
easygui.msgbox("yes, yes it works")
value = easygui.enterbox("Redmine ticket number:")
easygui.textbox(title="Output", text="Data and text etc..")
# there is more on the man page
```
---
Work in progress...
