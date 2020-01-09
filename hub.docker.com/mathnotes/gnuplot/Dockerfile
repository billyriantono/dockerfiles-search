FROM mathnotes/jupyter:2019-08-21
MAINTAINER Ryan Jensen <ryan.jensen@mathnotes.cc>

USER root

## Install build dependencies
RUN apt-get update && \
  apt-get install -yq --no-install-recommends \
  gnuplot \
  gnuplot-data \
  gnuplot-doc \
  libzmq5 && \
	rm -rf /var/lib/apt/lists/*

## GNUplot Kernel
RUN pip3 install gnuplot_kernel

## Runtime configuration
USER $MN_USER
WORKDIR $MN_HOME
RUN python3 -m gnuplot_kernel install --user

CMD jupyter notebook \
  --no-browser \
  --ip=* \
  --port=8888 \
  --NotebookApp.token='' \
  --NotebookApp.password=''

## Expose ports
EXPOSE 8888
