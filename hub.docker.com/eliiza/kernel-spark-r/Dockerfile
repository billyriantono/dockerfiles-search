FROM eliiza/spark-base:latest

USER root
RUN apt update -y && \
    apt install -y libjq-dev libv8-3.14-dev libprotobuf-dev
USER jovyan

# then some R things...
COPY common-r/requirements.txt /tmp/requirements.txt
RUN conda update --yes conda && \
  conda install -c r --yes --file /tmp/requirements.txt && \
  conda clean -tipsy && \
  fix-permissions $CONDA_DIR

COPY common-r/install.R /tmp/install.R
RUN Rscript --slave --no-save --no-restore-history /tmp/install.R

#ENV R_LIBS_USER ${R_HOME}/library:${SPARK_HOME}/R/lib

# Install OOTB kernelspecs
COPY kernel-launchers /usr/local/share/jupyter/kernel-launchers/

# WORKDIR /home/jovyan
USER root
RUN chown -R jovyan:users \
    /usr/local/share/jupyter \
    /opt/spark/work-dir 
USER jovyan
