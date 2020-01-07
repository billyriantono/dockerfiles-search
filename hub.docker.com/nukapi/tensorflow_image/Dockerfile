FROM jupyter/scipy-notebook

# Install Tensorflow
RUN conda install --quiet --yes \
    'tensorflow=1.5.0' \
    'keras=2.1.4' && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
