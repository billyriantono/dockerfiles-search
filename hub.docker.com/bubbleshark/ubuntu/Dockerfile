FROM ubuntu:16.04
RUN apt-get update && apt-get install -y software-properties-common && add-apt-repository ppa:deadsnakes/ppa -y && apt-get update && apt-get install -y build-essential curl vim tmux python3.6 wget && rm -rf /var/lib/apt/lists/*
RUN curl https://bootstrap.pypa.io/get-pip.py -o /root/get-pip.py && ln -s /usr/bin/python3.6 /usr/bin/python && python /root/get-pip.py && rm /root/get-pip.py
ADD data/.vimrc /root/ 
ADD data/.vim /root/.vim
ADD data/.tmux.conf /root/

