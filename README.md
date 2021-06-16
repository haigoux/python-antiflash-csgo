# antiflash.py
antiflash.py - disable the effect of flashbangs using python in csgo.




## Usage

```python
import pymem
import requests


proc = pymem.Pymem("csgo.exe")
client = pymem.process.module_from_name(proc.process_handle, "client.dll").lpBaseOfDll
engine = pymem.process.module_from_name(proc.process_handle, "engine.dll" ).lpBaseOfDll

offsets = requests.get('https://raw.githubusercontent.com/frk1/hazedumper/master/csgo.json').json()
dwLocalPlayer = int(offsets['signatures']['dwLocalPlayer'])

while True:
    player= proc.read_int(client + dwLocalPlayer)
    proc.write_int(player + int(offsets['netvars']['m_flFlashDuration']), 0)

```
