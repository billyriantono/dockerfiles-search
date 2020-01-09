# FIXME: This image is from April 8 (https://github.com/jupyter/docker-stacks/commit/8a1b90cbcba5355e6174a9fc24fe225813befe92)
# Attempts to use newer versions - within a couple months of 9/18/2018 - were encountering this issue:
# https://github.com/jupyter/docker-stacks/issues/679 - r-notebook kernel crashes because of png support
# Ubuntu 16.04.4 LTS - Xenial
FROM jupyter/r-notebook:latest

# Additional package needed by launcher, update IRkernel to fix kernel shutdown.
COPY common-r/requirements.txt /tmp/requirements.txt
RUN conda update --yes conda && \
  conda install -c r --yes --file /tmp/requirements.txt && \
  conda clean -tipsy && \
  fix-permissions $CONDA_DIR

USER root
RUN apt update -y && \
    apt install -y libjq-dev \
      libv8-3.14-dev \
      protobuf-compiler \
      libprotobuf-dev \
      libudunits2-dev \
      libgdal-dev \
      libgdal20 \
      libgeos-dev
USER jovyan

COPY common-r/install.R /tmp/install.R
RUN Rscript --slave --no-save --no-restore-history /tmp/install.R

# Install OOTB kernelspecs
COPY kernel-launchers /usr/local/share/jupyter/kernel-launchers/
COPY kernel-launchers/bootstrap/bootstrap-kernel.sh /usr/local/bin/

# Switch back to root to create the kernel user
USER root

RUN chown jovyan:users /usr/local/bin/bootstrap-kernel.sh && \
	  chmod 0755 /usr/local/bin/bootstrap-kernel.sh && \
    chown -R jovyan:users /usr/local/share/jupyter

USER jovyan
