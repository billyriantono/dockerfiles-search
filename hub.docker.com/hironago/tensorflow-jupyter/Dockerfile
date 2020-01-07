FROM python:3.5.4
LABEL maintainer 'nago3<jou.seek.5.f.it.inf@gmail.com>'

# Dependencies
RUN apt-get update && \
    apt-get install -y build-essential libpng12-dev libffi-dev
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# TensorFlow
ENV TENSORFLOW_V 1.4.1
RUN pip --no-cache-dir \
    install https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-${TENSORFLOW_V}-cp35-cp35m-linux_x86_64.whl

# Python library
RUN pip --no-cache-dir install \
      keras sklearn jupyter ipykernel scipy \
      simpy matplotlib numpy pandas plotly \
      sympy librosa Pillow h5py
RUN python -m ipykernel.kernelspec

# Jupyter Notebook config
ENV CONFIG /root/.jupyter/jupyter_notebook_config.py
ENV CONFIG_IPYTHON /root/.ipython/profile_default/ipython_config.py
RUN jupyter notebook --generate-config --allow-root && ipython profile create
RUN echo "c.NotebookApp.ip = '*'" >>${CONFIG}
RUN echo "c.NotebookApp.open_browser = False" >>${CONFIG}
RUN echo "c.InteractiveShellApp.exec_lines = ['%matplotlib inline']" >>${CONFIG_IPYTHON}

# tensorboard port
EXPOSE 6006
# ipython port
EXPOSE 8888

VOLUME /notebooks

# Run Jupyter Notebook
WORKDIR "/notebooks"
CMD ["jupyter","notebook", "--allow-root", "--ip=0.0.0.0"]
