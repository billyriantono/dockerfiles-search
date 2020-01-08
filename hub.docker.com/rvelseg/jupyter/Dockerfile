FROM jupyter/datascience-notebook

LABEL mantainer "Roberto Velasco Segura <roberto.velasco@icat.unam.mx>"

USER root

ENV HOME /root/

WORKDIR /tmp

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential make \
        octave liboctave-dev \
        gnuplot-x11 \
        libopenblas-base libatlas3-base \
        ghostscript pstoedit python3-pip less \
	&& rm -rf /var/lib/apt/lists/*

RUN octave --eval 'pkg install -forge control signal'

RUN conda config --add channels conda-forge && \
    conda install --quiet --yes octave_kernel && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

RUN conda create --quiet --yes -p $CONDA_DIR/envs/python2 python=2.7 \
    ipython ipykernel kernda numpy scipy matplotlib && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

RUN $CONDA_DIR/envs/python2/bin/python -m ipykernel install && \
    $CONDA_DIR/envs/python2/bin/kernda -o -y /usr/local/share/jupyter/kernels/python2/kernel.json && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

RUN conda install --quiet --yes nb_conda nb_conda_kernels && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

RUN pip install gnuplot_kernel && \
    python -m gnuplot_kernel install && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

RUN rm -rf /tmp/* /var/tmp/*

ENV HOME /home/jovyan/

WORKDIR $HOME

# Switch back to jovyan to avoid accidental container runs as root
USER $NB_UID
