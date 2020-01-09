FROM jupyter/scipy-notebook:265297f221de
ARG JUPYTERHUB_VERSION=0.9.1
RUN pip install --no-cache \
    jupyterhub==$JUPYTERHUB_VERSION \ 
    faodata==1.1  \ 
    wbdata==0.2.7 \
    reportlab==3.5.6 \ 
    colour==0.1.5 \ 
    pyproj==1.9.5.1 \ 
    pillow==5.2.0 \ 
    holoviews==1.10.7 \ 
    country_converter==0.6.6 \ 
    lxml==4.2.4 
    
    

    

USER root

# R pre-requisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-dejavu \
    fonts-open-sans \
    tzdata \
    gfortran \
    gcc && apt-get clean && \
    rm -rf /var/lib/apt/lists/*
 
USER $NB_UID

# R packages including IRKernel which gets installed globally.
RUN conda install --quiet --yes \
    'phantomjs' \
    'rpy2=2.8*' \
    'r-base=3.4.1' \
    'r-irkernel=0.8*' \
    'r-plyr=1.8*' \
    'r-devtools=1.13*' \
    'r-tidyverse=1.1*' \
    'r-shiny=1.0*' \
    'r-rmarkdown=1.8*' \
    'r-forecast=8.2*' \
    'r-rsqlite=2.0*' \
    'r-reshape2=1.4*' \
    'r-nycflights13=0.2*' \
    'r-caret=6.0*' \
    'r-rcurl=1.95*' \
    'r-crayon=1.3*' \
    'r-randomforest=4.6*' \
    'r-htmltools=0.3*' \
    'r-sparklyr=0.7*' \
    'r-htmlwidgets=1.0*' \
    'r-hexbin=1.27*' && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
  
  
  
  
  
CMD ["jupyterhub-singleuser"]
