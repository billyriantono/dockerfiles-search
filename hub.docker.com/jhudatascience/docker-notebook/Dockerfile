FROM jupyter/datascience-notebook

# Install additional dependencies
RUN conda install --quiet --yes \
    'graphviz' && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR

RUN pip install graphviz

# Run without token since this notebook is only intended for local use
CMD ["start-notebook.sh", "--NotebookApp.token=''"]