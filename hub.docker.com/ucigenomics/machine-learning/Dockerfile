FROM ucigenomics/ghtf-r3.5-jpy-singlecell

RUN conda install pytorch torchvision cudatoolkit=9.0 -c pytorch && \
    	conda install -c anaconda tensorflow-gpu && \
	conda clean -tipsy && \
	fix-permissions $CONDA_DIR	

RUN conda create --quiet --yes -p $CONDA_DIR/envs/python2 python=2.7 ipython ipykernel kernda && \
	conda clean -tipsy

RUN . /opt/conda/etc/profile.d/conda.sh && \
	conda activate $CONDA_DIR/envs/python2 && \
	conda install pytorch torchvision cudatoolkit=9.0 -c pytorch && \
	conda install -c anaconda tensorflow-gpu && \
        conda clean -tipsy && \
        fix-permissions $CONDA_DIR/envs/python2

RUN . /opt/conda/etc/profile.d/conda.sh && \
	conda activate python2 && \
	conda install -c darts-comp-bio darts_dnn && \
	conda clean -tipsy && \
	python -m ipykernel install --user && \
	fix-permissions $CONDA_DIR

USER root

# Create a global kernelspec in the image and modify it so that it properly activates
# the python2 conda environment.
RUN . /opt/conda/etc/profile.d/conda.sh && \
        conda activate python2 && \
	$CONDA_DIR/envs/python2/bin/python -m ipykernel install && \
    	$CONDA_DIR/envs/python2/bin/kernda -o -y /usr/local/share/jupyter/kernels/python2/kernel.json &

USER $NB_USER
