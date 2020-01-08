FROM python
RUN apt-get update
RUN apt-get -y install nodejs vim zsh
RUN pip install -U pip
RUN pip install numpy scipy matplotlib pandas cython jupyterlab requests
RUN git clone --depth=1 https://github.com/robbyrussell/oh-my-zsh.git /root/.oh-my-zsh
RUN mkdir -p /root/jupyterlab

WORKDIR /root/jupyterlab
COPY jupyter_notebook_config.py /root/.jupyter/jupyter_notebook_config.py
COPY .zshrc /root/.zshrc

# Expose Jupyter port & cmd
EXPOSE 8888
# CMD jupyter-lab
ENTRYPOINT jupyter-lab