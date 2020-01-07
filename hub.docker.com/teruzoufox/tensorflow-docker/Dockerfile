FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04

# バージョン
ENV PYTHON_VERSION 3.7.3
ENV TENSORFLOW_VERSION 1.13.1

# apt-get
RUN apt-get update && \
    apt-get install -y software-properties-common \
                       tzdata
RUN apt-add-repository -y ppa:git-core/ppa && \
    apt-get update && \
    apt-get install -y git \
                       vim
RUN apt-get install -y make build-essential libssl-dev zlib1g-dev \
                       libbz2-dev libreadline-dev libsqlite3-dev wget \
                       curl llvm libncurses5-dev xz-utils tk-dev \
                       libxml2-dev libxmlsec1-dev libffi-dev

# Pythonインストール
RUN git clone https://github.com/pyenv/pyenv.git ~/.pyenv
RUN echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc && \
    echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
RUN echo 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bashrc
ENV PATH $PATH:/root/.pyenv/bin
RUN pyenv install ${PYTHON_VERSION} && \
    pyenv global ${PYTHON_VERSION} && \
    pyenv rehash
ENV PATH $PATH:/root/.pyenv/shims

# pipアップデート
RUN pip install --upgrade pip


# TensorFlowインストール
RUN pip --no-cache-dir install \
    https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-${TENSORFLOW_VERSION}-cp37-cp37m-linux_x86_64.whl

# pip
RUN pip --no-cache-dir install \
        keras \
        sklearn \
        jupyter \
        ipykernel \
        scipy \
        simpy \
        pandas \
        numpy \
        matplotlib \
        && \
    python -m ipykernel.kernelspec

# Jupyter Notebook設定
ENV CONFIG /root/.jupyter/jupyter_notebook_config.py
ENV CONFIG_IPYTHON /root/.ipython/profile_default/ipython_config.py 

RUN jupyter notebook --generate-config --allow-root && \
    ipython profile create

RUN echo "c.NotebookApp.ip = '0.0.0.0'" >>${CONFIG} && \
    echo "c.NotebookApp.port = 8888" >>${CONFIG} && \
    echo "c.NotebookApp.open_browser = False" >>${CONFIG} && \
    echo "c.NotebookApp.iopub_data_rate_limit=10000000000" >>${CONFIG} && \
    echo "c.MultiKernelManager.default_kernel_name = 'python3'" >>${CONFIG} 
RUN echo "c.InteractiveShellApp.exec_lines = ['%matplotlib inline']" >>${CONFIG_IPYTHON}

# 作業ディレクトリ作成
RUN mkdir /notebooks

# Jupyter Notebook起動
WORKDIR /notebooks
CMD ["jupyter","notebook", "--allow-root"]
