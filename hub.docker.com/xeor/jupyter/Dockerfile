FROM jupyter/minimal-notebook:latest

USER root
RUN echo \

    # bash kernel
    && pip install bash_kernel \
    && python -m bash_kernel.install \
    && chown -R jovyan: /home/jovyan/.local

USER jovyan
RUN echo \

    # https://github.com/jupyter/dashboards
    && pip install jupyter_dashboards \
    && jupyter dashboards quick-setup --sys-prefix \

    && conda install -c conda-forge jupyter_contrib_nbextensions \
    && conda install nb_conda
