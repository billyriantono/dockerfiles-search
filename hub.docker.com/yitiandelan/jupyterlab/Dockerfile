FROM jupyter/scipy-notebook

MAINTAINER TIANLAN <yitiandelan@outlook.com>

RUN conda install --quiet --yes \
    'nodejs' \
    'phantomjs' && \
    conda update --all --quiet --yes && \
    python3 -m pip install jupyter_c_kernel bash_kernel && \
    python3 -m ipykernel install --user && \
    python3 -m bash_kernel.install --user && \
    install_c_kernel --user && \
    jupyter labextension install --no-build jupyterlab-drawio && \
    jupyter labextension install --no-build @mflevine/jupyterlab_html && \
    jupyter lab build && \
    conda clean -tipsy && \
    npm cache clean --force && \
    rm -rf $CONDA_DIR/share/jupyter/lab/staging && \
    rm -rf /home/$NB_USER/.cache/yarn && \
    rm -rf /home/$NB_USER/.node-gyp
