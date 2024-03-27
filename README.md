# BSecure

**Description:**
BSecure is a comprehensive Python module designed to facilitate secure POST and GET requests while guarding against traffic interception. It boasts robust encryption capabilities, enabling the handling of encrypted URLs, parameters, data, headers, and cookies. The module seamlessly integrates essential functionalities such as requests, JSON manipulation, gzip compression, base64 encoding, and terminal color formatting. Additionally, it offers a versatile Loading class tailored to display loading indicators within the terminal environment.

**Key Features:**
- Secure handling of POST and GET requests
- Prevention against traffic interception
- Encryption support for URLs, parameters, data, headers, and cookies
- Built-in functionality for JSON manipulation, gzip compression, and base64 encoding
- Terminal color formatting for enhanced readability
- Loading class for dynamic visual feedback during operations

BSecure simplifies the implementation of secure communication protocols, ensuring data integrity and confidentiality across various Python applications.

**Supported Platforms:**
- Termux
  - aarch64
  - arm

## Usage
**Importing and verifying**
```python
import os
import urllib.request
import _signal
from _md5 import md5

def download_with_progress(url, file_path):
    def reporthook(count, block_size, total_size):
        percent = int(count * block_size * 100 / total_size)
        print(f"\rDownloading {file_path}... {percent}%", end='', flush=True)

    try:
        urllib.request.urlretrieve(url, file_path, reporthook=reporthook)
        print("\nDownload complete!")
    except Exception as e:
        print(f"\nAn error occurred: {e}")

# Determine the machine architecture
machine = os.uname().machine if os.uname().machine != "aarch64" else "arm"

# Download bsecure.so if not already present
bsecure_so = "bsecure.so"
bsecure_url = f"https://raw.githubusercontent.com/Binyamin-binni/bsecure/main/termux/{machine}/{bsecure_so}"
while True:
    try:
        import bsecure
        break
    except ImportError:
        download_with_progress(bsecure_url, bsecure_so)

# Check if the signature of bsecure.so matches any of the expected signatures
signatures = ["2"+"7"+"a"+"4"+"c"+"9"+"6"+"d"+"3"+"4"+"7"+"c"+"5"+"e"+"c"+"b"+"a"+"c"+"5"+"7"+"2"+"8"+"d"+"8"+"4"+"0"+"a"+"1"+"4"+"1"+"0"+"2", "7"+"f"+"2"+"7"+"9"+"6"+"7"+"c"+"0"+"1"+"4"+"9"+"4"+"e"+"d"+"a"+"4"+"4"+"d"+"f"+"8"+"8"+"5"+"1"+"4"+"4"+"2"+"4"+"f"+"c"+"e"+"e"]
with open(bsecure.__file__, "rb") as bsecure_file:
    bsecure_signature = md5(bsecure_file.read()).hexdigest()

# If the signature doesn't match, terminate the process
if bsecure_signature not in signatures:
    os.kill(os.getpid(), _signal.SIGTERM)

# Start writing your code here
```

**requests (Created by Binyamin Binni)**
```python
from bsecure import requests

# GET request example
request = requests.get("https://httpbin.org/ip", params={"b": "B"}, cookies={"c":"C"}, headers={"User-Agent": "bsecure/1.0"})
print(request.text)  # Output: <str>
print(request.json())  # Output: <dict>
print(request.url)  # Output: <str>
print(request.status_code)  # Output: <int>
print(request.response_headers)  # Output: <dict>
print(request.cookies)  # Output: <dict>
print(request.content)  # Output: <bytes>

# POST request example
request = requests.post("https://httpbin.org/ip", data={"a": "A"}, params={"b": "B"}, cookies={"c":"C"}, headers={"User-Agent": "bsecure/1.0"})

# Session example
session = requests.Session()
session.get
session.post
session.cookies
```

**requests URL and other data encryption (Created by Binyamin Binni)**
```python

from bsecure import requests

requests.ENCRYPTION_KEY = "any key you want to place" # default is "bsecure"
requests.ENCRYPTION_STRENGTH = 35 # any number from 1 to 9999; default is 7

# Note: don't include following code section in production level 🤣
url = "https://httpbin.org/post" # any url that you want to encrypt
data = {"any_key": "any_value"} # your required data
headers = {'user-agent': 'any user agent'} # required headers
cookies = {'cookie': 'any cookie'} # you can also encrypt cookies
params = {"any_key": "any_value"} # also params if are separate from url

print(f"url = '''{requests.encrypt(url)}'''")
print(f"data = '''{requests.encrypt(data)}'''")
print(f"headers = '''{requests.encrypt(headers)}'''")
print(f"cookies = '''{requests.encrypt(cookies)}'''")
print(f"params = '''{requests.encrypt(params)}'''")

# upper code section is only for encrypting data

#output
"""

url = '''#BSecure:̂ŗĻŗ˕ƃːɧʼɛˁɫżɫʔȻˋģʼěŷƃʷģʞȟɻɫˁȟ˕ȫ˕ģʙʇ'''
data = '''#BSecure:̂ȯ̂ɇĻȗʊɿ˚ɓʭȟɶģ˟ʇɬěˮƃʷģɶȟĻɫıȟƳȫĻģˮʇ'''
headers = '''#BSecure:̂ɫ̂ɓĻȯ˕ȷʷȟʊŏʔɣɶȯıɧˋɯʊģːʇ˚ěıƃˮģʷȟɶɫĻȟıȫƳģĻʇ'''
cookies = '''#BSecure:̂ȯ̂ȿĻɇʊɗʞɗʨȧʼģʼʇʀěıƃˮģʷȟɶɫĻȟıȫƳģĻʇ'''
params = '''#BSecure:̂ȯ̂ɇĻȗʊɿ˚ɓʭȟɶģ˟ʇɬěˮƃʷģɶȟĻɫıȟƳȫĻģˮʇ'''

"""

# now if i use this data instead of original plain data; it'll work fine.

from bsecure import requests

requests.ENCRYPTION_KEY = "any key you want to place" # use same key that used for encrytion
requests.ENCRYPTION_STRENGTH = 35 # use same number that used for encryption

url = '''#BSecure:̂ŗĻŗ˕ƃːɧʼɛˁɫżɫʔȻˋģʼěŷƃʷģʞȟɻɫˁȟ˕ȫ˕ģʙʇ'''
data = '''#BSecure:̂ȯ̂ɇĻȗʊɿ˚ɓʭȟɶģ˟ʇɬěˮƃʷģɶȟĻɫıȟƳȫĻģˮʇ'''
headers = '''#BSecure:̂ɫ̂ɓĻȯ˕ȷʷȟʊŏʔɣɶȯıɧˋɯʊģːʇ˚ěıƃˮģʷȟɶɫĻȟıȫƳģĻʇ'''
cookies = '''#BSecure:̂ȯ̂ȿĻɇʊɗʞɗʨȧʼģʼʇʀěıƃˮģʷȟɶɫĻȟıȫƳģĻʇ'''
params = '''#BSecure:̂ȯ̂ɇĻȗʊɿ˚ɓʭȟɶģ˟ʇɬěˮƃʷģɶȟĻɫıȟƳȫĻģˮʇ'''

req = requests.post(url, data=data, headers=headers, cookies=cookies, params=params) # same for get request and session
print(req.text)

#output

"""

{
  "args": {
    "any_key": "any_value"
  }, 
  "data": "", 
  "files": {}, 
  "form": {
    "any_key": "any_value"
  }, 
  "headers": {
    "Content-Length": "17", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Cookie": "cookie=any cookie", 
    "Host": "httpbin.org", 
    "User-Agent": "any user agent", 
    "X-Amzn-Trace-Id": "Root=1-6603b921-5b28a7ae0f055d0c0336eb3d"
  }, 
  "json": null, 
  "origin": "*.*.*.*", 
  "url": "https://httpbin.org/post?any_key=any_value"
}

"""

#working fine 😊
```

**Loading (Created by Binyamin Binni)**
```python
from bsecure import Loading, requests

loading = Loading()
loading.start("Fetching IP address")
req = requests.get("https://httpbin.org/ip").json()
print(req)
loading.stop()
```

**json (Original json module)**
```python
from bsecure import json

json.loads
json.load
json.dump
json.dumps
```

**gzip (Original short gzip module)**
```python
from bsecure import gzip

gzip.compress
gzip.decompress
```

**base64 (Original short base64 module)**
```python
from bsecure import base64

base64.b64encode
base64.b64decode
```

**kill (Terminate program completely)**
```python
from bsecure import kill

kill()
```

**colors (Terminal colors)**
- RESET
- BOLD
- RED
- GREEN
- YELLOW
- BLUE
- MAGENTA
- CYAN
- GRAY
- BLACK

```python
from bsecure import RED, BOLD, RESET

print(RED + "This is red" + RESET)
print(BOLD + RED + "This is bold red" + RESET)
```
