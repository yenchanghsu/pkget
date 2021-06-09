## VLNCE preparation (https://github.com/jacobkrantz/VLN-CE)
### Issue: import magnum in python shows "libOpenGL.so.0 is not found"
Solution:

1. Before creating the conda env for vlnce, do the steps here first.

2. Add this into .bashrc:
```bash
export PATH=.apt/usr/lib/x86_64-linux-gnu:$PATH
```

3. Copy pkget
```bash
wget https://raw.githubusercontent.com/0x00009b/pkget/master/pget && chmod +x pget
source .bashrc
```

4. Install libOpenGL0

You will find the installed libOpenGL.so.0 in ~.apt/usr/lib/x86_64-linux-gnu

```bash
./pget libOpenGL0
source .bashrc
```

5. Follow the installation instruction of VLN-CE
