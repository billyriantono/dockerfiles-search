FROM continuumio/miniconda3:latest

# use aliyun mirror
RUN echo "deb http://mirrors.aliyun.com/debian stretch main contrib non-free" > /etc/apt/sources.list && \
    echo "deb-src http://mirrors.aliyun.com/debian stretch main contrib non-free" >> /etc/apt/sources.list  && \
    echo "deb http://mirrors.aliyun.com/debian stretch-updates main contrib non-free" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.aliyun.com/debian stretch-updates main contrib non-free" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.aliyun.com/debian-security stretch/updates main contrib non-free" >> /etc/apt/sources.list


RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -

# nodejs/npm is only for jupyter lab plugin install
RUN apt-get update && apt-get install -y npm nodejs

RUN conda install jupyterlab xeus-cling -c conda-forge

# RUN jupyter labextension install @oriolmirosa/jupyterlab_materialdarker

# USER $NB_USER

RUN pip install bash_kernel
RUN python -m bash_kernel.install

ENV PORT=1080

CMD jupyter lab --port ${PORT} --ip=0.0.0.0 --allow-root --no-browser \
    --notebook-dir=/data/ \
    --config=/config/jupyter_notebook_config.py
