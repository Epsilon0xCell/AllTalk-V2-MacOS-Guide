# AllTalkv2_MacGuide
Updated Guide to installing AllTalk v2 on macOS

```
brew install espeak ffmpeg gcc git curl
xcode-select --install
git clone -b alltalkbeta https://github.com/erew123/alltalk_tts
cd alltalk_tts
mkdir alltalk_environment
cd alltalk_environment
curl -LO https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh
bash Miniconda3-latest-MacOSX-arm64.sh -b -p $PWD/conda
./conda/bin/conda create --no-shortcuts -y -k --prefix ../env python=3.11.9
source ./conda/bin/activate ../env
./conda/bin/conda install -y pytorch==2.3.0 torchvision==0.18.0 torchaudio==2.3.0 -c pytorch
./conda/bin/conda install -y -c conda-forge faiss-cpu
./conda/bin/conda install -y -c conda-forge "ffmpeg=*=*gpl*"
cd ..
nano -w system/requirements/requirements_standalone.txt
# Change onnxruntime-gpu>=1.18.1 to onnxruntime>=1.18.1 
pip install -r system/requirements/requirements_standalone.txt
pip install --upgrade gradio==4.19.2
pip install -r system/requirements/requirements_parler.txt
./alltalk_environment/conda/bin/conda clean --all --force-pkgs-dirs -y
pip install --upgrade transformers==4.37.2
```
