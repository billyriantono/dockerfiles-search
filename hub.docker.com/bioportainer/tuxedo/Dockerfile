FROM bioportainer/pyenv:cpu

RUN eval "$(pyenv init -)" \
    && eval "$(pyenv virtualenv-init -)" \
    && pyenv activate $PYTHON3_VERSION \
    && conda install readline=6.2 bwa bowtie2 tophat cufflinks -y \
    && conda clean -tipsy && pyenv deactivate
