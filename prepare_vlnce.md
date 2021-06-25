## VLNCE preparation without sudo (https://github.com/jacobkrantz/VLN-CE)
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
./pget libopengl0
source .bashrc
```

5. Follow the installation instruction of VLN-CE

### Issue: "Can not get default EGL display: EGL_BAD_PARAMETER"
```bash
# replace the libnvidia-gl with the version that matches your driver version
./pget libnvidia-gl-418=418.87.00-0ubuntu1
```
## VLNCE installation with sudo
```bash
sudo apt-get install libopengl0
sudo apt-get install libnvidia-gl-418=418.87.00-0ubuntu1
conda create -n vlnce python3.6
conda activate vlnce
git clone --branch stable https://github.com/facebookresearch/habitat-lab.git
cd habitat-lab
pip install -r requirements.txt
python setup.py develop --all # install habitat and habitat_baselines
git clone https://github.com/jacobkrantz/VLN-CE.git
cd VLN-CE
python -m pip install -r requirements.txt
```
Test:

Download the [test scenes data](http://dl.fbaipublicfiles.com/habitat/habitat-test-scenes.zip) and extract data folder in zip to habitat-lab/data/ where habitat-lab/ is the github repository folder.

Run the example script python examples/example.py which in the end should print out number of steps agent took inside an environment (eg: Episode finished after 2 steps.). To verify that tests pass run python setup.py test which should print out a log about passed, skipped and failed tests.

Issue:
nvidia-smi shows "Failed to initialize NVML: Driver/library version mismatch". But habitat seems to work fine.
