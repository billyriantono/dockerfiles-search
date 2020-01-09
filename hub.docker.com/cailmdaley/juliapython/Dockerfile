FROM cailmdaley/juliabase:latest

USER root
RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential  \
        libbz2-dev       \
        libffi-dev       \
        liblzma-dev      \
        libncurses5-dev  \
        libreadline-dev  \
        libssl-dev       \
        libsqlite3-dev   \
        nodejs           \
        npm              \
        tk-dev           \
        xz-utils         \
        zlib1g-dev       \
    && rm -rf /var/lib/apt/lists/*
user $IMAGEUSER

# install python with pyenv since we need a dynamically-linked executable so
# that PyJulia works
ENV PYENV_ROOT $SRC/.pyenv
ENV PATH="$PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH"
RUN curl https://pyenv.run | bash \
    && CFLAGS="-O2" PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install 3.7.3 \
    && pyenv global 3.7.3

# install Python packages
RUN pip install --no-cache-dir \
        git+https://github.com/JuliaPy/pyjulia.git \
        jupyterlab \
        matplotlib \
        numpy \
        pip \
        scipy \
    && rm -rf $HOME/.cache


# Jupyter setup
ENV JUPYTER_PATH $SRC/.jupyter
ENV JUPYTER_CONFIG_DIR $JUPYTER_PATH
COPY --chown=1000 jupyter_notebook_config.py $JUPYTER_CONFIG_DIR/
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout $JUPYTER_CONFIG_DIR/jupyter.key \
    -out    $JUPYTER_CONFIG_DIR/jupyter.cert \
    -subj "/C=US/ST=Illinois/O=SPT/CN=Cail Daley"

# install Python-Julia packages
RUN julia -e 'using Pkg; pkg"add PyCall PyPlot IJulia; precompile"'




CMD jupyter lab
