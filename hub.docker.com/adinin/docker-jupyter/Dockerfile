FROM jupyter/scipy-notebook


# Install Tensorflow
RUN conda install --yes \
    'tensorflow=1.6*' \
    'keras=2.0*' && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER


RUN pip install protobuf ipywidgets google && conda install --yes protobuf 

RUN jupyter nbextension enable --py --sys-prefix widgetsnbextension

