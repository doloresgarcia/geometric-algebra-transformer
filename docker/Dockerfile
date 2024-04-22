FROM nvidia/cuda:11.7.1-base-ubuntu20.04

RUN apt update && \
    DEBIAN_FRONTEND=noninteractive apt install --yes --no-install-recommends \
        build-essential \
        cmake \
        ffmpeg \
        git \
        python-is-python3 \
        python3-dev \
        python3-pip \
        && \
    rm -rf /var/lib/apt/lists/*
 
COPY docker/requirements.txt requirements.txt

RUN python3 -m pip install --no-cache-dir --upgrade pip && \
    python3 -m pip install --no-cache-dir --upgrade --requirement requirements.txt
RUN python3 -m pip install --no-cache-dir pyg_lib torch_scatter torch_sparse torch_cluster torch_spline_conv -f https://data.pyg.org/whl/torch-2.0.0+cu117.html
RUN python3 -m pip install pyg_lib torch_scatter torch_sparse torch_cluster torch_spline_conv -f https://data.pyg.org/whl/torch-1.13.1+cu117.html
RUN python3 -m pip install pytorch-lightning yacs torchmetrics
RUN python3 -m pip install performer-pytorch
RUN python3 -m pip install tensorboardX
RUN python3 -m pip install ogb
RUN python3 -m pip install wandb
RUN python3 -m pip install seaborn
RUN python3 -m pip install  dgl -f https://data.dgl.ai/wheels/cu117/repo.html
RUN python3 -m pip install numpy
RUN python3 -m pip install scipy
RUN python3 -m pip install pandas
RUN python3 -m pip install scikit-learn
RUN python3 -m pip install matplotlib
RUN python3 -m pip install tqdm
RUN python3 -m pip install PyYAML
RUN python3 -m pip install awkward0
RUN python3 -m pip install uproot
RUN python3 -m pip install awkward
RUN python3 -m pip install vector
RUN python3 -m pip install lz4
RUN python3 -m pip install xxhash
RUN python3 -m pip install tables
RUN python3 -m pip install tensorboard
COPY docker/ext_packages /docker/ext_packages
RUN python3 /docker/ext_packages/install_upstream_python_packages.py

COPY . /gatr/
RUN python3 -m pip install --no-cache-dir /gatr && rm -rf /gatr

# RUN apt-get install -y git
# RUN mkdir /opt/pepr
# RUN cd /opt/pepr && git clone https://github.com/cms-pepr/pytorch_cmspepr.git
# RUN cd /opt/pepr/pytorch_cmspepr && FORCE_CUDA=1 TORCH_CUDA_ARCH_LIST="8.0 8.0" python3 -m pip install -e .

