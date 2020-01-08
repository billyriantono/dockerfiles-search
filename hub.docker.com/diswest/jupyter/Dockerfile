FROM python:3.6
MAINTAINER Ivan Miniailenko <discrete.west@gmail.com>

RUN apt-get update && \
    apt-get install -y pandoc texlive-xetex && \
    apt-get clean

RUN pip install --no-cache-dir \
        jupyter \
        keras \
        matplotlib \
        numpy \
        pandas \
        scipy \
        scikit-learn \
        seaborn \
        sqlalchemy \
        tensorflow \
        ujson \
        xgboost

RUN apt-get update && \
    apt-get install -y cmake && \
    git clone --recursive https://github.com/Microsoft/LightGBM.git /home/lightgdm && \
    cd /home/lightgdm && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make -j4 && \
    cd /home/lightgdm/python-package && \
    python setup.py install && \
    apt-get remove -y cmake && \
    apt-get clean

RUN jupyter notebook --generate-config --allow-root && \
    sed -i "s/#c.NotebookApp.token = '<generated>'/c.NotebookApp.token = ''/" ~/.jupyter/jupyter_notebook_config.py && \
    mkdir /notebooks

# http://jupyter-notebook.readthedocs.io/en/latest/public_server.html#docker-cmd
ENV TINI_VERSION v0.14.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini

VOLUME /notebooks

RUN mkdir /tflog
VOLUME /tflog
ENV TF_LOG_PATH /tflog

EXPOSE 8888

ENTRYPOINT ["/usr/bin/tini", "--"]
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--allow-root", "--ip=0.0.0.0", "--notebook-dir=/notebooks"]
