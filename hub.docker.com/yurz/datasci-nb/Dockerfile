FROM jupyter/scipy-notebook:latest
LABEL authors="Yuri Zhylyuk yuri@zhylyuk.com"

ARG NB_USER=jovyan

USER root

RUN \
    apt-get update \
    && apt-get -y upgrade \
    && apt-get -y install apt-utils sshpass wget libpq-dev bzip2 pkg-config \
        libzmq3-dev git smbclient tzdata \
    && apt-get -y install --reinstall ca-certificates \
    && update-ca-certificates

ENV TZ Australia/Melbourne

USER ${NB_USER}
RUN \ 
    mkdir ${HOME}/notebooks \
    && conda update conda \
    && conda install -y -c conda-forge numpy pip pandas \
        pysftp pysmbclient pytz \
        psycopg2 pymysql mysql pymssql \
        SQLAlchemy requests lxml openpyxl xlsxwriter xlrd \
        dask distributed numba \ 
        boto3 azure \
        seaborn plotly \
        vaex \
        # matplotlib seaborn plotly holoviews bokeh datashader \
        # dash dash_core_components \
        # graphviz \
        # scikit-learn keras tensorflow nltk textblob dask-ml lightfm \
    && conda install -y -c pyviz pyviz \
    && pip install --upgrade pip \
        git+https://bitbucket.org/yurz/datautils-python \
        git+https://bitbucket.org/yurz/c3py \
        cufflinks pdvega \
        jupyterthemes \
        modin \
        # dash_html_components python-telegram-bot \
    && jupyter nbextension install --sys-prefix --py vega3 \
    # && jupyter labextension install @mflevine/jupyterlab_html jupyterlab-drawio @jupyterlab/plotly-extension \
    && jt -t onedork -fs 12 -altp -tfs 11 -nfs 115 -cellw 96% -T -N 

#### Cleanup
##############################
USER root
RUN \
    conda clean -y -a && \
    apt-get clean autoclean && \
    apt-get autoremove -y && \
    rm -rf /var/lib/{cache,log}/
RUN chown -R ${NB_USER} /home/${NB_USER}


USER ${NB_USER}
WORKDIR ${HOME}/notebooks

# docker build -t yurz/datasci-nb:latest .
