FROM fastgenomics/jupyter-base:0.1.9

COPY requirements_conda.txt requirements_pip.txt /tmp/

# Add channles in such order that the highest priority comes last

RUN conda config --add channels bioconda --add channels conda-forge && \
	conda install -q --file /tmp/requirements_conda.txt && \
	conda clean -afy && \
	pip install --upgrade pip && \
	pip install -r /tmp/requirements_pip.txt

# install JupyterLab Extension
RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager

# run jupyter lab build just to make sure everything is up-to-date after package install
RUN jupyter lab build
