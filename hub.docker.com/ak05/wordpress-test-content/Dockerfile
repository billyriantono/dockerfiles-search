ARG BASE_CONTAINER=jupyter/pyspark-notebook
FROM $BASE_CONTAINER


RUN conda install --quiet -y tensorflow pytorch findspark && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER


# RUN conda install --file requirements.txt