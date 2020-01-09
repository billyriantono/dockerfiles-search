# Base Image
FROM jupyter/base-notebook

# Maintainer
LABEL maintainer "Shiho ASA"

# Configure environment
ENV CONDA_DIR=/opt/conda \
    NB_USER=jovyan
    
# Install Jupyter Notebook and Hub
RUN conda install --quiet --yes \
#    'numpy=1.13.*' \
    'numpy=*' \
#    'scipy=0.19.*' \
    'scipy=*' \    
#    'sympy=1.1.*' \
    'sympy=*' \    
#    'matplotlib=2.1.*' \
    'matplotlib=*' \    
    && conda clean -tipsy && \
    fix-permissions $CONDA_DIR

# Install Sample Notebook
COPY sample_notebook/CavityFlow_with_Navier-Stokes.ipynb /home/$NB_USER/
