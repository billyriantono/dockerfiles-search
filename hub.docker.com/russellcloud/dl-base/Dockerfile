FROM russellcloud/dl-deps:latest-py2
MAINTAINER RussellCloud Team "support@russellcloud.cn"

RUN pip --no-cache-dir install \
        Cython \
        h5py \
        ipykernel \
        jupyter \
        matplotlib \
        numpy \
        pandas \
        path.py \
        pyyaml \
        scipy \
        six \
        sklearn \
        sympy \
        Pillow \
        zmq \
        && \
    python -m ipykernel.kernelspec

# Set up our notebook config.
COPY jupyter_notebook_config_py2.py /root/.jupyter/
RUN mv /root/.jupyter/jupyter_notebook_config_py2.py /root/.jupyter/jupyter_notebook_config.py 

# Jupyter has issues with being run directly:
#   https://github.com/ipython/ipython/issues/7062
# We just add a little wrapper script.
COPY run_jupyter.sh /
RUN chmod +x /run_jupyter.sh

# IPython
EXPOSE 8888

CMD ["/run_jupyter.sh"]