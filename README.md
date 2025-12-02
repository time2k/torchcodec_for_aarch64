#torchcodec PIP wheels for Nvidia DGX Spark
git clone https://github.com/meta-pytorch/torchcodec.git

sed -i 's/requires *= *\["setuptools>=61.0"\]/requires = ["setuptools>=61.0", "torch", "pybind11"]/g' pyproject.toml

sudo apt update && sudo apt install -y \
    libavdevice-dev \
    libavfilter-dev \
    libavformat-dev \
    libavcodec-dev \
    libavutil-dev \
    libswresample-dev \
    libswscale-dev

export CUDA_HOME=/usr/local/cuda
export PATH=$CUDA_HOME/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/lib:$CUDA_HOME/lib:$CUDA_HOME/lib64:$LD_LIBRARY_PATH

#ENABLE_CUDA=1 pip install -e . --no-build-isolation
ENABLE_CUDA=1 I_CONFIRM_THIS_IS_NOT_A_LICENSE_VIOLATION=1 pip wheel . --no-build-isolation --verbose  --no-binary=flash_attn --wheel-dir=./wheels
