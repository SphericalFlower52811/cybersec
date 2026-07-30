# RCE via misconfigured python interpreter

## Details

I will just put the details of the exploit, as the code was from a few months ago and the vulnerability has already been patched.

## Exploitation

I used import platform; print(platform.system()) on the python interpreter to see Linux as the output. Additionally, the top of the editor said /root/main.py.

That seemed very suspicious, and I wondered if I really had root permissions.

I managed to find out that I was in a Docker, and managed to mount it with root permissions as the Docker container used was actually misconfigured.

After mounting the docker, I had access to all the files, including the database and source code.

## The Fix

Either properly configure your Docker and keep your user as a user with no permissions, or use Pyodide via WebAssembly (also properly configured) for a secure python interpreter.
