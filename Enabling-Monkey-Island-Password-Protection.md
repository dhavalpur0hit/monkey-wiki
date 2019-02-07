# Setting up authentication
By default, the Monkey Island doesn't require any form of authentication. To enable it, follow the following instructions:

### 1. Modify the server_config.json file

Modify the file `/monkey/monkey_island/cc/server_config.json` to be of the following format:

```
{
  "server_config": "password",
  "user": "<YOUR USER>",
  "hash": "<LOWER CASE HASH>"
}
```

* Replace `<YOUR USER>` with a username of your choice. e.g. `monkey`
* Replace `<LOWER CASE HASH>` with a lower case SHA3-512 hash of your password. e.g. `0123456789abcedf0123456789abcedf0123456789abcedf0123456789abcedf0123456789abcedf0123456789abcedf0123456789abcedf0123456789abcedf`

### 2. Restart Monkey Island
Restart the Monkey Island process.

# Computing SHA3-512
There are various libraries and services which allow to compute the SHA3-512. We'll list 2 tested services for convenience:

### 1. Using this free online tool
You can use [this](https://www.browserling.com/tools/sha3-hash) free online tool to calculate SHA3-512

### 2. Using PyCrypto / PyCryptodome
The [PyCrypto](https://pypi.org/project/pycrypto/)/[PyCryptodome](https://pycryptodome.readthedocs.io) library for python allows SHA3-512 computation.

The following snippet calculates the SHA3-512 of the `secret` variable:

```
from Crypto.Hash import SHA3_512
h = SHA3_512.new()
h.update(secret)
print(h.hexdigest())
```