FROM jupyter/datascience-notebook
LABEL maintainer="Tim Zhang"

# Install pyomo and its conditional dependencies
RUN conda install -c conda-forge pyomo
RUN conda install -c conda-forge pyomo.extras

# Install from requirements.txt file
COPY requirements.txt /tmp/
RUN pip install --requirement /tmp/requirements.txt && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
