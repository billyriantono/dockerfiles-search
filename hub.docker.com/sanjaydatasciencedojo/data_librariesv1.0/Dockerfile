# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
FROM jupyter/scipy-notebook

LABEL maintainer="Jupyter Project <jupyter@googlegroups.com>"

# Set when building on Travis so that certain long-running build steps can
# be skipped to shorten build time.
ARG TEST_ONLY_BUILD

USER root

# R pre-requisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-dejavu \
    tzdata \
    gfortran \
    gcc && apt-get clean && \
    rm -rf /var/lib/apt/lists/*


USER $NB_UID

# R packages including IRKernel which gets installed globally.
RUN conda install --quiet --yes \
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
RUN conda install --quiet --yes -c mittner r-animation && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR
RUN Rscript -e "install.packages('GGally',repos='https://cloud.r-project.org/')"
RUN Rscript -e "install.packages('glmnet',repos='https://cloud.r-project.org/',dependencies=TRUE)"
RUN Rscript -e "install.packages('tm',repos='https://cloud.r-project.org/')"
RUN Rscript -e "install.packages('lsa',repos='https://cloud.r-project.org/',dependencies=TRUE)"
RUN Rscript -e "install.packages('miscTools',repos='https://cloud.r-project.org/')"
RUN Rscript -e "install.packages('party',repos='https://cloud.r-project.org/',dependencies=TRUE)"
RUN Rscript -e "install.packages('bst',repos='https://cloud.r-project.org/',dependencies=TRUE)"
RUN Rscript -e "install.packages('AUC',repos='https://cloud.r-project.org/')"
RUN Rscript -e "install.packages('pROC',repos='https://cloud.r-project.org/')"
RUN Rscript -e "install.packages('e1071',repos='https://cloud.r-project.org/')"
RUN Rscript -e "install.packages('klaR',repos='https://cloud.r-project.org/',dependencies=TRUE)"
RUN Rscript -e "install.packages('Metrics',repos='https://cloud.r-project.org/')"
RUN Rscript -e "install.packages('fpc',repos='https://cloud.r-project.org/',dependencies=TRUE)"
RUN Rscript -e "install.packages('rpart.plot',repos='https://cloud.r-project.org/',dependencies=TRUE)"
RUN Rscript -e "install.packages('xgboost',repos='https://cloud.r-project.org/',dependencies=TRUE)"
RUN Rscript -e "install.packages('quanteda',repos='https://cloud.r-project.org/',dependencies=TRUE)"
RUN Rscript -e "install.packages('irlba',repos='https://cloud.r-project.org/')"
RUN Rscript -e "install.packages('doSNOW',repos='https://cloud.r-project.org/',dependencies=TRUE)"
RUN Rscript -e "install.packages('Rtsne',repos='https://cloud.r-project.org/',dependencies=TRUE)"



# Add Julia packages. Only add HDF5 if this is not a test-only build since
# it takes roughly half the entire build time of all of the images on Travis
# to add this one package and often causes Travis to timeout.
#
# Install IJulia as jovyan and then move the kernelspec out
# to the system share location. Avoids problems with runtime UID change not
# taking effect properly on the .local folder in the jovyan home dir.







 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
    
    
    
    
    
    
    
    
    
    
    
    
    
    
