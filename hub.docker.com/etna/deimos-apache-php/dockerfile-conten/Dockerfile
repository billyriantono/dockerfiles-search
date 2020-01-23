FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04
LABEL maintainer="picy2k@gmail.com"

ARG KUBECTL_VERSION=1.11.8
ARG HELM_VERSION=2.13.0
ARG JUPYTERHUB_VERSION=0.9.6
# ARG TENSORFLOW_VERSION=1.13.1
#ARG ACCELERATOR=cpu-mkl
# ARG ACCELARATOR=gpu-cuda10-tensorrt
# Python 3.7
ARG ANACONDA="https://repo.anaconda.com/archive/Anaconda3-2019.07-Linux-x86_64.sh"
ARG TENSORFLOW="https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.14.0-cp37-cp37m-linux_x86_64.whl"

# Python 3.6
# ARG ANACONDA="Anaconda3-5.0.1-Linux-x86_64.sh"

ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8
ENV TZ=Asia/Singapore
ENV TERM=xterm-256color
ENV SHELL=/bin/zsh

RUN echo $TZ > /etc/timezone

# apt packages
RUN apt-get -f -y upgrade && \
    apt-get clean && \
    apt-get update --fix-missing && \
    apt-get -f -y install \
        apt-transport-https \
        build-essential \
        binutils \
        bzip2 \
        ca-certificates \
        cmake \
        curl \
        g++ \
        gcc \
        git \
        groff \
        file \
        fonts-powerline \
        htop \
        locales \
        libglib2.0-0 \
        libpq-dev \
        libxext6 \
        libsm6 \
        libxrender1 \
        libxt-dev \
        locales \
        make \
        mercurial \
        python-pip \
        python3-pip \
        openjdk-8-jdk-headless \
        ruby  \
        ruby-all-dev \
        screenfetch \
        software-properties-common \
        subversion \
        sudo \
        tree \
        tmux \
        tzdata \
        uuid-runtime \
        wget \
        zsh \
        zlib1g-dev \
    && add-apt-repository ppa:neovim-ppa/stable && apt-get update && apt-get -f -y install neovim && \
    apt-get clean

# timezone
RUN rm /etc/localtime && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata && \
    apt-get clean && \
    echo "LC_ALL=en_US.UTF-8" >> /etc/environment && \
    echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
    echo "LANG=en_US.UTF-8" > /etc/locale.conf && \
    locale-gen en_US.UTF-8 && \
    localedef -i en_US -f UTF-8 en_US.UTF-8

# MOOTD
WORKDIR /tmp
RUN wget https://github.com/busyloop/lolcat/archive/master.zip && \
    unzip master.zip && \
    cd lolcat-master/bin && \
    gem install lolcat && \
    git clone https://github.com/etheleon/beesay.git /tmp/beesay && \
    cd /tmp/beesay && \
    ./setup.py --without-info --freedom=partial install && \
    mkdir /tmp/innermessage && \
    cp /etc/update-motd.d/* /tmp/innermessage && \
    rm -rf /etc/update-motd.d/* && \
    cp -r /tmp/innermessage /etc/update-motd.d/innermessage && \
    cp /tmp/beesay/extras/logo.sh /etc/update-motd.d/innermessage/ && \
    cp /tmp/beesay/extras/05-screenfetch /etc/update-motd.d/innermessage/ && \
    cp /tmp/beesay/extras/10-help-text /etc/update-motd.d/innermessage/ && \
    echo '#!/bin/sh\nrun-parts /etc/update-motd.d/innermessage | lolcat -f | ponysay -f airasia -W 300 --balloon round' | tee /etc/update-motd.d/50-ponysay && \
    chmod +x /etc/update-motd.d/50-ponysay

#############################################################################
# Customization
#############################################################################

# user jovyan
RUN useradd -m -s /bin/zsh jovyan \
    && echo 'jovyan ALL=(ALL) NOPASSWD:ALL' >>/etc/sudoers

USER jovyan
WORKDIR /home/jovyan

# oh-my-zsh
RUN sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" && \
    wget https://raw.githubusercontent.com/etheleon/dotfiles/master/.zshrc  -O - >> $HOME/.zshrc && \
    echo "/etc/update-motd.d/50-ponysay\n" >> $HOME/.zshrc && \
    git clone https://github.com/etheleon/.tmux.git && \
    ln -s -f .tmux/.tmux.conf && \
    cp .tmux/.tmux.conf.local .

# linuxbrew
RUN git clone https://github.com/Linuxbrew/brew.git /home/jovyan/.linuxbrew
ENV PATH=/home/jovyan/.linuxbrew/bin:/home/jovyan/.linuxbrew/sbin:$PATH
RUN brew update
ENV MANPATH="$(brew --prefix)/share/man:$MANPATH" \
    INFOPATH="$(brew --prefix)/share/info:$INFOPATH"

# anaconda
ENV PATH=/home/jovyan/anaconda3/bin:$PATH
RUN wget --quiet $ANACONDA -O ~/anaconda.sh && \
    /bin/bash ~/anaconda.sh -b -p /home/jovyan/anaconda3 && \
    rm ~/anaconda.sh && \
    conda install -y -q \
        numpy \
        tqdm && \
    pip install --no-cache-dir \
      autopep8 \
      awscli \
      ciso8601 \
      findspark \
      feather-format \
      jupyter_client \
      nbresuse \
      neovim \
      psycopg2 \
      reprexpy \
      sklearn_pandas \
      scikit-surprise \
      swifter \
      tzlocal \
      xgboost

# git
RUN wget https://raw.githubusercontent.com/etheleon/dotfiles/master/.gitconfig -O - > $HOME/.gitconfig

# editor
RUN brew install --HEAD universal-ctags/universal-ctags/universal-ctags && \
    brew install ack fzf && \
    $(brew --prefix)/opt/fzf/install && \
    sudo ln -s /home/jovyan/.linuxbrew/bin/ctags /usr/bin/ctags && \
    echo "set keymap vi-command\n" >> $HOME/.inputrc && \
    echo "set editing-mode vi" >> $HOME/.inputrc && \
    echo "Control-l: clear-screen\n" >> $HOME/.inputrc && \
    echo "set keymap vi-insert\n" >> $HOME/.inputrc && \
    echo "Control-l: clear-screen\n" >> $HOME/.inputrc && \
    echo "bindkey -v\n" >> $HOME/.zshrc && \
    echo "bindkey '^R' history-incremental-search-backward" >> $HOME/.zshrc && \
    git clone https://github.com/etheleon/nvim.git $HOME/.config/nvim && \
    echo | echo | nvim -i NONE -c PlugInstall -c quitall && \
    echo | echo | nvim -i NONE -c UpdateRemotePlugins -c quitall

# kubernetes
# HB kubectl <= 1.10.5
# HB helm == 2.8.2
# kubectx and kube-ps1
RUN mkdir -p $HOME/local/kubectl/bin $HOME/local/helm/bin/ $HOME/local/kubectx/bin && \
    sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add - && \
    sudo echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list && \
    sudo apt update && \
    sudo apt install -y kubectl=${KUBECTL_VERSION}-00 && sudo mv /usr/bin/kubectl /usr/bin/kubectl-${KUBECTL_VERSION} && \
    sudo apt install -y --allow-downgrades kubectl=1.10.5-00 && sudo mv /usr/bin/kubectl /usr/bin/kubectl-1.10.5 && \
    sudo update-alternatives --install $HOME/local/kubectl/bin/kubectl kubectl /usr/bin/kubectl-${KUBECTL_VERSION} 20 && \
    sudo update-alternatives --install $HOME/local/kubectl/bin/kubectl kubectl /usr/bin/kubectl-1.10.5 10 && \
    wget https://storage.googleapis.com/kubernetes-helm/helm-v${HELM_VERSION}-linux-amd64.tar.gz && \
    wget https://storage.googleapis.com/kubernetes-helm/helm-v2.8.2-linux-amd64.tar.gz && \
    mkdir helm-2.8.2 && tar -zvxf helm-v2.8.2-linux-amd64.tar.gz -C $PWD/helm-2.8.2 && \
    mkdir helm-${HELM_VERSION} && tar -zvxf helm-v${HELM_VERSION}-linux-amd64.tar.gz -C $PWD/helm-${HELM_VERSION} && \
    sudo mv helm-${HELM_VERSION}/linux-amd64/helm /usr/local/bin/helm-${HELM_VERSION} && \
    sudo mv helm-2.8.2/linux-amd64/helm /usr/local/bin/helm-2.8.2 && \
    rm helm-v${HELM_VERSION}-linux-amd64.tar.gz helm-v2.8.2-linux-amd64.tar.gz && \
    rm -r helm-2.8.2 && \
    rm -r helm-${HELM_VERSION} && \
    sudo update-alternatives --install $HOME/local/helm/bin/helm helm /usr/local/bin/helm-${HELM_VERSION} 20 && \
    sudo update-alternatives --install $HOME/local/helm/bin/helm helm /usr/local/bin/helm-2.8.2 10 && \
    git clone https://github.com/jonmosco/kube-ps1.git /home/jovyan/local/kube-ps1/ && \
    git clone https://github.com/ahmetb/kubectx.git && \
    cp kubectx/kubectx $HOME/local/kubectx/bin && \
    cp kubectx/kubens $HOME/local/kubectx/bin && \
    rm -rf kubectx && \
    mkdir -p $HOME/local/k9s/bin && \
    cd $HOME/local/k9s/bin && \
    wget https://github.com/derailed/k9s/releases/download/0.7.13/k9s_0.7.13_Linux_x86_64.tar.gz && \
    tar zvxf k9s_0.7.13_Linux_x86_64.tar.gz && \
    cd $HOME

# ipython jupyter
RUN pip install --no-cache-dir --upgrade \
       jupyter \
       notebook==5.7.8 \
       jgscm \
       google-cloud==0.32.0 \
       git+https://github.com/etheleon/s3contents \
       git+https://github.com/quantopian/pgcontents \
       jupyterhub==$JUPYTERHUB_VERSION && \
    git clone https://github.com/ipython-contrib/jupyter_contrib_nbextensions.git && \
    pip install -e jupyter_contrib_nbextensions && \
    # rm -rf jupyter_contrib_nbextensions && \
    jupyter contrib nbextension install --sys-prefix && \
    ipython profile create && \
    echo "c.InteractiveShellApp.extensions = ['autoreload', 'rpy2.ipython', 'sparkmagic.magics']\n" >> $HOME/.ipython/profile_default/ipython_config.py && \
    echo "c.InteractiveShellApp.exec_lines = ['%autoreload 2']\n" >> $HOME/.ipython/profile_default/ipython_config.py && \
    echo "c.InteractiveShellApp.exec_lines.append('print(\"Warning: disable autoreload in ipython_config.py to improve performance.\")')\n" >> $HOME/.ipython/profile_default/ipython_config.py && \
    echo "c.TerminalInteractiveShell.editing_mode = 'vi'\n" >> $HOME/.ipython/profile_default/ipython_config.py

# R packages
RUN conda install -y rpy2 r-tidyverse r-devtools r-irkernel r-openssl r-sparklyr && \
    Rscript -e "install.packages('cowplot', repos='cran.rstudio.com/')" && \
    Rscript -e "install.packages('pbdZMQ', repos='cran.rstudio.com/')" && \
    Rscript -e "install.packages('skimr', repos='cran.rstudio.com/')" && \
    Rscript -e "install.packages('rstudioapi', repos='cran.rstudio.com/')"


ENV TAR=/bin/tar

# spark
RUN R -e 'sparklyr::spark_install(version="2.4.0", hadoop_version="2.7")' && \
    wget http://central.maven.org/maven2/com/amazonaws/aws-java-sdk/1.7.4/aws-java-sdk-1.7.4.jar -P /home/jovyan/spark/spark-2.4.0-bin-hadoop2.7/jars/ && \
    wget http://central.maven.org/maven2/org/apache/hadoop/hadoop-aws/2.7.3/hadoop-aws-2.7.3.jar -P /home/jovyan/spark/spark-2.4.0-bin-hadoop2.7/jars/ && \
    cp /home/jovyan/spark/spark-2.4.0-bin-hadoop2.7/conf/spark-defaults.conf.template /home/jovyan/spark/spark-2.4.0-bin-hadoop2.7/conf/spark-defaults.conf && \
    echo "spark.hadoop.fs.s3a.impl        org.apache.hadoop.fs.s3a.S3AFileSystem" >> /home/jovyan/spark/spark-2.4.0-bin-hadoop2.7/conf/spark-defaults.conf

ENV PATH "$PATH:/home/jovyan/spark/spark-2.4.0-bin-hadoop2.7/bin/"
ENV SPARK_HOME "$HOME/spark/spark-2.4.0-bin-hadoop2.7"

# jupyter config
RUN mkdir $HOME/.jupyter && \
    wget https://raw.githubusercontent.com/etheleon/dotfiles/master/jupyter_notebook_config.py -O - > $HOME/.jupyter/jupyter_notebook_config.py

# spark magic
RUN mkdir $HOME/.sparkmagic/ && \
    wget https://raw.githubusercontent.com/etheleon/dotfiles/master/jupyter_sparkmagic_config.json -O - > $HOME/.sparkmagic/config.py && \
    pip install --no-cache-dir \
        autovizwidget \
        widgetsnbextension \
        hdijupyterutils && \
    git clone https://github.com/etheleon/sparkmagic.git && \
    cd sparkmagic/sparkmagic && \
    pip install . && \
    cd /home/jovyan && rm -rf sparkmagic

# jupyter extensions
RUN jupyter nbextension enable codefolding/main && \
    jupyter serverextension enable --py nbresuse --sys-prefix && \
    jupyter nbextension install --py nbresuse --sys-prefix && \
    jupyter nbextension enable --py nbresuse --sys-prefix && \
    jupyter nbextension enable toc2/main && \
    jupyter nbextension enable execute_time/ExecuteTime && \
    jupyter nbextension enable livemdpreview/livemdpreview

# install and configure deeplearning tf, keras
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
# ENV WHL=https://github.com/mind/wheels/releases/download/tf${TENSORFLOW_VERSION}-${ACCELARATOR}/tensorflow-${TENSORFLOW_VERSION}-cp36-cp36m-linux_x86_64.whl
RUN pip install --no-cache-dir --upgrade $TENSORFLOW jupyter-tensorboard
RUN mkdir $HOME/.keras && echo '{ "image_data_format": "channels_last", "epsilon": 1e-07, "floatx": "float32", "backend": "tensorflow" }' > $HOME/.keras/keras.json

RUN cd /tmp && \
    wget --quiet https://github.com/krallin/tini/releases/download/v0.18.0/tini && \
    sudo mv tini /usr/local/bin/tini && \
    sudo chmod +x /usr/local/bin/tini

ENTRYPOINT ["tini", "-g", "--"]
CMD ["start-singleuser.sh"]

RUN echo 'jupyterhub-singleuser --ip="0.0.0.0" --port=8888' > start-singleuser.sh && \
    sudo mv start-singleuser.sh /usr/local/bin/start-singleuser.sh && \
    sudo chown jovyan:users /usr/local/bin/start-singleuser.sh && \
    sudo chmod +x /usr/local/bin/start-singleuser.sh

# gcloud
RUN curl -sSL https://sdk.cloud.google.com > /tmp/gcl && bash /tmp/gcl --install-dir=$HOME/local --disable-prompts

# terraform
RUN mkdir -p $HOME/local/terraform/bin && \
    cd $HOME/local/terraform/bin && \
    wget https://releases.hashicorp.com/terraform/0.12.6/terraform_0.12.6_linux_amd64.zip && \
    unzip terraform_0.12.6_linux_amd64.zip
