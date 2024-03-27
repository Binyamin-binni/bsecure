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

## Supported Platforms
- Termux
  - aarch64
  - arm

## Included Modules and Functions

### requests (Created by Binyamin Binni)
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

### Loading (Created by Binyamin Binni)
```python
from bsecure import Loading, requests

loading = Loading()
loading.start("Fetching IP address")
req = requests.get("https://httpbin.org/ip").json()
print(req)
loading.stop()
```

### json (Original json module)
```python
from bsecure import json

json.loads
json.load
json.dump
json.dumps
```

### gzip (Original short gzip module)
```python
from bsecure import gzip

gzip.compress
gzip.decompress
```

### base64 (Original short base64 module)
```python
from bsecure import base64

base64.b64encode
base64.b64decode
```

### kill (Terminate program completely)
```python
from bsecure import kill

kill()
```

### colors (Terminal colors)
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

## NOTE
```python
# Verify the signature of the module after importing to prevent tampering
from _md5 import md5
import os
import _signal
import bsecure

# Retrieve the signature of the module
arm_signature = "SIGNATURE OF ARM SHARED MODULE PRESENT IN signature FILE"
aarch64_signature = "SIGNATURE OF AARCH64 SHARED MODULE PRESENT IN signature FILE"
bsecure_signature = md5(open(bsecure.__file__, "rb").read()).hexdigest()

# Compare the signatures and terminate the program if they do not match
if os.uname().machine == "aarch64":
    if bsecure_signature != aarch64_signature:
        os.kill(os.getpid(), _signal.SIGTERM)
else:
    if bsecure_signature != arm_signature:
        os.kill(os.getpid(), _signal.SIGTERM)
```
