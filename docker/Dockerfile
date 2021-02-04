FROM nvidia/cuda:8.0-cudnn6-devel 

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
         build-essential \
         git \
         curl \
         ca-certificates \
         libjpeg-dev \
         libpng-dev \
         python3-pip \
         python3-dev \
         python3-setuptools\
         libxkbcommon-x11-0 \
         libsm6\ 
         libxext6\
         libxrender-dev\
         swig \
         eog\ 
         tmux\
         nano\
         htop\
         wget\
         && rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade "pip < 21.0"
RUN pip3 install torch==0.4.1 torchvision
RUN pip3 install opencv-python==4.2.0.34

RUN pip3 install cython scipy matplotlib pycocotools sklearn tqdm packaging pyyaml
RUN pip3 install tensorboard cffi

# enables tmux to use mouse
RUN echo "set -g mouse on" > ~/.tmux.conf

# enable pdb autocomplete
RUN  printf "import rlcompleter\nimport pdb\npdb.Pdb.complete = rlcompleter.Completer(locals()).complete" > ~/.pdbrc

WORKDIR "/root/giou_faster_rcnn/"