# AllTalkv2_MacGuide
Updated Guide to installing AllTalk v2 on macOS

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install espeak ffmpeg gcc git curl espeakng
xcode-select --install
git clone -b alltalkbeta https://github.com/erew123/alltalk_tts
cd alltalk_tts
mkdir alltalk_environment
cd alltalk_environment
curl -LO https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh
bash Miniconda3-latest-MacOSX-arm64.sh -b -p $PWD/conda
./conda/bin/conda create --no-shortcuts -y -k --prefix ../env python=3.11.9
source ./conda/bin/activate ../env
./conda/bin/conda install -y pytorch==2.2.1 torchvision==0.17.1 torchaudio==2.2.1 -c pytorch
./conda/bin/conda install -y -c conda-forge faiss-cpu
./conda/bin/conda install -y -c conda-forge "ffmpeg=*=*gpl*"
cd ..
nano -w system/requirements/requirements_standalone.txt
# Change onnxruntime-gpu>=1.18.1 to onnxruntime>=1.18.1

# Interesting Part: Obtain the wheel file from here:
https://github.com/rhasspy/piper-phonemize/issues/14#issuecomment-2094395478 && https://github.com/rhasspy/piper-phonemize/files/15210981/piper_phonemize-1.1.0-cp311-cp311-macosx_11_0_arm64.whl.zip
unzip in the alltalk_enviornment and then pip install piper_phonemize-1.1.0-cp311-cp311-macosx_11_0_arm64.whl

^ Follow the compile steps if you do not trust the wheel file.

pip install -r system/requirements/requirements_standalone.txt
pip install --upgrade gradio==4.32.2
pip install -r system/requirements/requirements_parler.txt
./alltalk_environment/conda/bin/conda clean --all --force-pkgs-dirs -y
pip install --upgrade transformers==4.42.4
pip install pip==24.0
pip install git+https://github.com/liyaodev/fairseq.git
python script.py (select XTTS v2)
```
