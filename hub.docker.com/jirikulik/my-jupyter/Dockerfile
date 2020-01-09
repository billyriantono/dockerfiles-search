#copied and adjusted from jupyter/scipy-notebook

FROM continuumio/miniconda3

ENV CONDA_DIR=/opt/conda \
    SHELL=/bin/bash \
    NB_USER=jovyan \
    NB_UID=1000 \
    NB_GID=100
ENV HOME=/home/$NB_USER

RUN groupadd wheel -g 11 && \
    echo "auth required pam_wheel.so use_uid" >> /etc/pam.d/su && \
    useradd -m -s /bin/bash -N -u $NB_UID $NB_USER && \
    chown $NB_USER:$NB_GID $CONDA_DIR && \
    chmod g+w /etc/passwd

RUN conda update conda
RUN conda update python
RUN conda install --yes \
    'blas=*=openblas' numpy scipy scikit-learn && \
    conda clean -tipsy && \
#RUN conda remove --yes --force qt pyqt
    pip install --upgrade --no-cache-dir pip && \
    pip install -U --no-cache-dir \
    pandas \
    deap sklearn-deap \
    alpha_vantage \
    simplejson \
    pyzmq

USER $NB_UID
#USER root

# libav-tools for matplotlib anim
#RUN apt-get update \
#    #&& apt-get install -y --no-install-recommends libav-tools \
#    && apt-get install -y --no-install-recommends ffmpeg \
#    && apt-get install -y --no-install-recommends openssh-client \
#    && apt-get install -y --no-install-recommends curl \
#    && curl -sSL https://sdk.cloud.google.com > /home/$NB_USER/gclinst && bash /home/$NB_USER/gclinst --install-dir=/usr/gcloud --disable-prompts \
#    && rm -rf /home/$NB_USER/gclinst \
#    && apt-get clean \
#    && rm -rf /var/lib/apt/lists/*

#ENV PATH="/usr/gcloud/google-cloud-sdk/bin:${PATH}"

#USER $NB_UID

# Install Python 3 packages
# Remove pyqt and qt pulled in for matplotlib since we're only ever going to
# use notebook-friendly backends in these images
#RUN conda install --quiet --yes \
#    'blas=*=openblas' \
#    #'ipywidgets' \
#    'pandas' \
#    'matplotlib' \
#    'scipy' \
#    'scikit-learn' \
	#'bqplot' \
#	'deap' \
    #'sympy' && \
#    && conda remove --quiet --yes --force qt pyqt \
#    && conda clean -tipsy \
#    # Activate ipywidgets extension in the environment that runs the notebook server
    #jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
    # Also activate ipywidgets extension for JupyterLab
    #jupyter labextension install @jupyter-widgets/jupyterlab-manager@^0.35 && \
	#Mine follows
    #jupyter labextension install bqplot && \
#	&& pip install --upgrade pip \
#	&& pip install -U --no-cache-dir sklearn-deap alpha_vantage yellowbrick simplejson pyzmq \
    #python -m pip install pymongo && \
    #pip install tinydb --no-cache-dir && \
    #pip install sacred --no-cache-dir && \
    #pip install tinydb-serialization --no-cache-dir && \
    #pip install hashfs --no-cache-dir && \
    #pip install google-cloud-bigquery --no-cache-dir && \
#    && pip install -U --no-cache-dir mysql-connector-python update_checker tqdm stopit xgboost tpot google-auth google-auth-httplib2 google-api-python-client \
#    && npm install -g ungit \
    #curl -SL https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-203.0.0-linux-x86_64.tar.gz
	#End of mine
#    && npm cache clean --force && \
#    rm -rf $CONDA_DIR/share/jupyter/lab/staging && \
#    rm -rf /home/$NB_USER/.cache/yarn \
#    && rm -rf /home/$NB_USER/.node-gyp \
#    && fix-permissions $CONDA_DIR \
#    && fix-permissions /home/$NB_USER \
#    && fix-permissions /home/jovyan/.config/gcloud

# Install facets which does not have a pip or conda package at the moment
#RUN cd /tmp && \
#    git clone https://github.com/PAIR-code/facets.git && \
#    cd facets && \
#    jupyter nbextension install facets-dist/ --sys-prefix && \
#    cd && \
#    rm -rf /tmp/facets && \
#    fix-permissions $CONDA_DIR && \
#    fix-permissions /home/$NB_USER

# Import matplotlib the first time to build the font cache.
#ENV XDG_CACHE_HOME /home/$NB_USER/.cache/
#RUN MPLBACKEND=Agg python -c "import matplotlib.pyplot" && \
#    fix-permissions /home/$NB_USER

#USER $NB_UID



#FROM continuumio/miniconda3

#RUN /opt/conda/bin/conda update -n base conda && \
#	/opt/conda/bin/conda install -y -c conda-forge numpy scikit-learn pandas nodejs jupyterlab ipywidgets bqplot deap && \
#	jupyter labextension install @jupyter-widgets/jupyterlab-manager && \
#	jupyter labextension install bqplot && \
#	/opt/conda/bin/conda clean -tipsy && \
#	pip install --upgrade pip && \
#	pip install sklearn-deap --no-cache-dir && \
#	pip install alpha_vantage --no-cache-dir && \
#	pip install -U yellowbrick --no-cache-dir

#RUN ["mkdir", "notebooks"]
#
#EXPOSE 8888
#
#VOLUME /notebooks
#
#ENTRYPOINT [ "/usr/bin/tini", "--" ]
#CMD [ "/bin/bash" ]