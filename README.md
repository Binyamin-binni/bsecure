# BSecure
## Description
*bsecure* is a module designed for secure POST and GET requests with traffic capturing prevention. It provides features such as handling data parameters, headers, cookies, sessions, as well as secure JSON encoding/decoding, gzip compression, base64 encoding, and terminal color formatting. Additionally, it includes a Loading class for displaying loading indicators in the terminal.

## Supported Platforms
1. Termux
   * aarch64
   * arm

## Includes
> ### requests (Created by Binyamin Binni)
> ```
> from bsecure import requests
> request = requests.get("https://httpbin.org/ip", params={"b": "B"}, cookies={"c":"C"}, headers={"User-Agent": "bsecure/1.0"})
> request.text # <str>
> request.json() # <dict>
> request.url # <str>
> request.status_code # <int>
> request.response_headers # <dict>
> request.cookies # <dict>
> request.content # <bytes>
>
> request = requests.post("https://httpbin.org/ip", data={"a": "A"}, params={"b": "B"}, cookies={"c":"C"}, headers={"User-Agent": "bsecure/1.0"})
>
> session = requests.Session()
> session.get
> session.post
> session.cookies
> ```
> ### Loading (Created by Binyamin Binni)
> ```
> from bsecure import Loading, requests
> loading = Loading()
> loading.start("Fetching ip address")
> req = requests.get("https://httpbin.org/ip").json()
> print(req)
> loading.stop()
> ```
> ### json (Original json module)
> ```
> from bsecure import json
> json.loads
> json.load
> json.dump
> json.dumps
> ```
> ### gzip (Original short gzip module)
> ```
> from bsecure import gzip
> gzip.compress
> gzip.decompress
> ```
> ### base64 (Original short base64 module)
> ```
> from bsecure import base64
> base64.b64encode
> base64.b64decode
> ```
> ### kill (Terminate program completely)
> ```
> from bsecure import kill
> kill()
> ```
> ### colors (Termial colors)
> * RESET
> * BOLD
> * RED
> * GREEN
> * YELLOW
> * BLUE
> * MAGENTA
> * CYAN
> * GRAY
> * BLACK
> ```
> from bsecure import RED, BOLD, RESET
> print(RED + "This is red" + RESET)
> print(BOLD + RED + "This is bold red" + RESET)
## NOTE
> ```
> # verify the signature of module after importing to prevent tempering
> from _md5 import md5
> import os
> import _signal
> import bsecure
> arm_signature = "SIGNATURE OF ARM SHARED MODULE PRESENT IN signature FILE"
> aarch64_signature = "SIGNATURE OF AARCH64 SHARED MODULE PRESENT IN signature FILE"
> bsecure_signature = md5(open(bsecure.__file__, "rb").read()).hexdigest()
> if os.uname().machine == "aarch64":
>   if bsecure_signature != aarch64_signature:
>     os.kill(os.getpid(), _signal.SIGTERM)
> else:
>   if bsecure_signature != arm_signature:
>     os.kill(os.getpid(), _signal.SIGTERM)
> ```
