# https://hub.docker.com/r/naruya/
# 5900: VNC, 8888: jupyter, 6006: tensorboard
# $ docker run --runtime=nvidia -it --privileged -p 5900:5900 -p 8888:8888 -p 6006:6006 naruya/dl_remote

# [1] https://github.com/robbyrussell/oh-my-zsh
# [2] https://github.com/pyenv/pyenv/wiki/common-build-problems

FROM nvidia/cudagl:9.2-devel-ubuntu18.04
ENV DEBIAN_FRONTEND=noninteractive

# zsh,[1] ----------------
RUN apt-get update -y && apt-get -y upgrade && apt-get install -y \
    wget curl git zsh
SHELL ["/bin/zsh", "-c"]
RUN wget http://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh

# pyenv,[2] ----------------
RUN apt-get update -y && apt-get -y upgrade && apt-get install -y \
    make build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
    libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl git
RUN curl https://pyenv.run | zsh && \
    echo '' >> /root/.zshrc && \
    echo 'export PATH="/root/.pyenv/bin:$PATH"' >> /root/.zshrc && \
    echo 'eval "$(pyenv init -)"' >> /root/.zshrc && \
    echo 'eval "$(pyenv virtualenv-init -)"' >> /root/.zshrc
RUN source /root/.zshrc && \
    pyenv install 3.7.4 && \
    pyenv global 3.7.4

# X window ----------------
RUN apt-get update && apt-get install -y xvfb x11vnc python-opengl

# --------------------------------
# additional (highly recommended)
# --------------------------------

RUN apt-get update && apt-get install -y vim

# python, jupyter
RUN apt-get update && apt-get install -y ffmpeg nodejs npm
RUN source /root/.zshrc && \
    pip install -U setuptools && \
    pip install moviepy jupyterlab && \
    pip install torch==1.3.1+cu92 torchvision==0.4.2+cu92 -f https://download.pytorch.org/whl/torch_stable.html && \
    pip install tensorflow-gpu==2.0.0 && \
    echo 'alias jl="DISPLAY=:0 jupyter lab --ip 0.0.0.0 --port 8888 --allow-root &"' >> /root/.zshrc && \
    echo 'alias tb="tensorboard --logdir runs --bind_all &"' >> /root/.zshrc

# window manager
RUN apt-get update && apt-get install -y icewm

# OpenAI Gym
RUN source /root/.zshrc && \
    pip install gym

RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /root
CMD ["zsh"]