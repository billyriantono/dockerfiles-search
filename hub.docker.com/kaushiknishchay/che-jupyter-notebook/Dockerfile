FROM ksmster/s2i-minimal-notebook:v1

ENV HOME_DIR=$HOME
ENV JUPYTER_DIR=${HOME_DIR}/.jupyter

RUN mkdir -p ${JUPYTER_DIR}/custom

COPY custom.js ${JUPYTER_DIR}/custom
