FROM jupyter/tensorflow-notebook

WORKDIR /home/jovyan

USER root
RUN sudo apt-get update && apt-get install -y \
   vim \
   tig \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

USER jovyan
RUN jupyter contrib nbextension install --user
RUN git clone https://github.com/lambdalisue/jupyter-vim-binding.git ./.local/share/jupyter/nbextensions/usability/vim_binding
USER root
RUN chmod -R go-w ./.local/share/jupyter/nbextensions/usability/vim_binding
COPY ./jupyter_notebook_config.py ./.jupyter/
COPY ./nbconfig ./.jupyter/nbconfig

COPY requirements_option.txt ./
RUN pip install --no-cache-dir -r requirements_option.txt
RUN sudo apt-get update && apt-get install -y \
   graphviz \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*

WORKDIR /home/jovyan/jupyter
