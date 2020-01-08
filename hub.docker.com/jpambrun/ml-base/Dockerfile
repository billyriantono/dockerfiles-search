FROM ubuntu:18.04

# Install tini
ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV SHELL /bin/bash

RUN apt-get update --fix-missing && \
    apt-get install -y \
	 wget \
 	 bzip2 \
         ca-certificates \
	 python3 \
	 python3-dev \
	 python3-distutils \
         curl \
	 wget \
         git \
	 vim \
         build-essential \
         silversearcher-ag \
	 parallel \
         && \ 
    apt-get clean && \ 
    rm -rf /var/lib/apt/lists/*

RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash - && \
    apt-get install -y nodejs && \
    apt-get clean && \ 
    rm -rf /var/lib/apt/lists/*

RUN wget -O ~/get-pip.py https://bootstrap.pypa.io/get-pip.py && \
    python3.6 ~/get-pip.py && \
    ln -s /usr/bin/python3.6 /usr/local/bin/python && \
    pip install \
         setuptools \
         && \
    pip install \
        python-language-server \
        flake8 \
        autopep8 \
        pylint 

RUN npm install -g yarn diff-so-fancy

RUN git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf && ~/.fzf/install

ENV NODE_PATH /usr/lib/node_modules/

RUN  echo "    IdentityFile ~/.ssh/id_rsa" >> /etc/ssh/ssh_config

ENTRYPOINT [ "/tini", "--" ]
CMD [ "/bin/bash" ]
