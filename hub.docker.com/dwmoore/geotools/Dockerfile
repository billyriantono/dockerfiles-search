FROM cyversevice/jupyterlab-scipy:latest
MAINTAINER Tyson Swetnam <tswetnam@cyverse.org>
#--- changes below : Daniel Moore  (dmoore@renci.org)
USER root
COPY environment.yml /environment.yml
RUN /opt/conda/bin/conda env update -n root -f /environment.yml
USER jovyan
