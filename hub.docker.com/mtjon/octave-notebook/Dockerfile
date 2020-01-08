FROM jupyter/minimal-notebook:8a1b90cbcba5

LABEL maintainer='Martin Tjon <martintjon@gmail.com>'

USER root

RUN apt-get update && \
    apt-get install -yq \
    octave

USER $NB_USER

RUN conda install -yq \
    octave_kernel \
    gnuplot && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR

CMD ["jupyter", "lab"]