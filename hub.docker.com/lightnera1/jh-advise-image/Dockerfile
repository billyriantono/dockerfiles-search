FROM jupyter/datascience-notebook:83ed2c63671f
ARG JUPYTERHUB_VERSION=0.9.4


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
    lxml==4.2.4 \ 
    regex==2018.08.29 \ 
    socrata-py==0.4.14 \ 
    psycopg2==2.7.5 \ 
    sodapy==1.4.7 \
    pyxlsb==1.0.3 \
    python-pptx==0.6.17 \ 
    shapely==1.6.4.post2 \ 
    geopandas==0.4.0 \
    jupyterlab_iframe==0.0.11 \
    jupyterlab_latex==0.4.1 \ 
    partd==0.3.9 \
    WeasyPrint 

    
    
    

    

USER root

# R pre-requisites, fonts, and additional ubuntu software for spell checker 
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-open-sans \
    automake \ 
    autopoint \ 
    libtool \
    graphviz \
    libncurses5-dev \
    libreadline-dev \
    libhunspell-dev \
    texlive-xetex \
    libcairo2 \
    libpango-1.0-0 \
    libpangocairo-1.0-0 \
    libgdk-pixbuf2.0-0 \
    libffi-dev \
    poppler-utils \
    shared-mime-info\
    libsnappy-dev  && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
  

USER $NB_USER


RUN conda install --quiet --yes \
    'phantomjs' 

# configure to open with documenation (add this line to the bottom of the config file)
RUN echo "" >> /etc/jupyter/jupyter_notebook_config.py
RUN echo "c.JupyterLabIFrame.welcome = 'https://data-services-docs.nanoapp.io/'" >> /etc/jupyter/jupyter_notebook_config.py


RUN jupyter labextension install @jupyterlab/toc \ 
    @jupyterlab/latex \
    @jupyterlab/git \
    @jupyterlab/celltags \
    @agoose77/jupyterlab-attachments \
    @ijmbarr/jupyterlab_spellchecker \
    jupyterlab_iframe \
    @mflevine/jupyterlab_html \
    https://github.com/lckr/jupyterlab-variableInspector \
    jupyterlab-drawio
    
  
RUN pip install jupyterlab-git \
    jupyter-server-proxy \
    python-snappy==0.5.3 \
    intake \ 
    fuzzywuzzy \ 
    hunspell \
    python-Levenshtein 
    
    
RUN jupyter serverextension enable --py jupyterlab_git \
    jupyterlab_iframe \
    jupyterlab_latex


CMD ["jupyterhub-singleuser"]
