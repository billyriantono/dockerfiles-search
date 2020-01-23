# Distributed under the terms of the Modified BSD License.
FROM rocker/verse:3.4.3

LABEL maintainer="Sang-Yun Oh <syoh@ucsb.edu>"

##
USER root

ENV SCRIPTDIR /home/rstudio/misc
ADD scripts ${SCRIPTDIR}
RUN chmod a+x ${SCRIPTDIR}/install_yadm.sh

##
USER rstudio

RUN ${SCRIPTDIR}/install_yadm.sh

RUN git config --global user.email "syoh@ucsb.edu"
RUN git config --global user.name "Sang-Yun Oh"
RUN git config --global credential.helper 'cache --timeout=3600'

RUN Rscript ${SCRIPTDIR}/Dockerfile.R

## built image doesn't run without below
USER root 

