FROM rowangaffney/data_science_im_rs_step1


USER root
RUN apt-get update && \
	apt-get install -y --no-install-recommends \
		libapparmor1 \
		libedit2 \
		lsb-release \
		psmisc \
		r-cran-rodbc \
		libclang-dev \
		systemd \
		libssl1.0.0

RUN RSTUDIO_PKG=rstudio-server-1.2.5019-amd64.deb && \
  wget -q https://download2.rstudio.org/server/trusty/amd64/${RSTUDIO_PKG} && \
  dpkg -i ${RSTUDIO_PKG} && \
  rm ${RSTUDIO_PKG} && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*
#/opt/conda/bin/python -m pip install git+https://github.com/jupyterhub/jupyter-rsession-proxy

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/*
    


USER $NB_UID

# R packages
# RUN conda update -n base conda --yes
RUN conda create -n R_geo --yes
RUN conda install -n R_geo -c r r-irkernel rstudio

RUN conda install -n R_geo -c conda-forge --quiet --yes \
  'r-rgdal' \
  'r-gdalutils' \
  'r-raster' \
  'r-snow' \
  'r-sf' \
  'r-gstat' \
  'r-maptools' \
  'r-rgeos' \
  'r-irkernel' \
  'r-reticulate' \
  'r-sp'
  
RUN conda run -n R_geo pip install git+https://github.com/jupyterhub/jupyter-rsession-proxy

#  'jupyter-rsession-proxy' \

#RUN pip install git+https://github.com/jupyterhub/jupyter-rsession-proxy
#RUN pip install jupyter-rsession-proxy \
#  && jupyter labextension install jupyterlab-server-proxy

#RUN jupyter labextension install jupyterlab_toastify @jupyterlab/server-proxy
#RUN conda run -n R_geo jupyter labextension install jupyterlab_toastify @jupyterlab/server-proxy

## FROM https://github.com/grst/rstudio-server-conda
# USER root
#RUN systemctl disable rstudio-server.service && \
#  systemctl stop rstudio-server.service

# RUN git clone https://github.com/grst/rstudio-server-conda.git

# RUN conda run -n R_geo ./start_rstudio_server.sh 6060

USER $NB_UID

#RUN conda install -c conda-forge --quiet --yes h5netcdf
#RUN pip install --quiet h5pyd
  
#RUN conda install -c conda-forge jupyter-rsession-proxy
#RUN jupyter labextension install @oriolmirosa/jupyterlab_materialdarker

#RUN conda config --add channels "conda-forge/label/cf201901"
#RUN conda install -n R_geo -c "conda-forge/label/cf201901" r-rgdal r-gdalutils

RUN fix-permissions /home/$NB_USER
RUN fix-permissions $CONDA_DIR

#RUN echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
#  echo "conda activate base" >> ~/.bashrc

#RUN echo "source /opt/conda/etc/profile.d/conda.sh" >> $SINGULARITY_ENVIRONMENT

#RUN conda init bash

ENV PATH="${PATH}:/usr/lib/rstudio-server/bin"
ENV LD_LIBRARY_PATH="/usr/lib/R/lib:/lib:/usr/lib/x86_64-linux-gnu:/usr/lib/jvm/java-7-openjdk-amd64/jre/lib/amd64/server:/opt/conda/envs/R_geo/lib/R/lib"


#RUN conda activate R_geo
#RUN Rscript -e "install.packages('neonUtilities',repos = 'http://cran.us.r-project.org')"

#USER root
#RUN rstudio-server verify-installation
#RUN rstudio-server restart

USER $NB_UID
