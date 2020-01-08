FROM mathnotes/base:2019-08-21
MAINTAINER Ryan Jensen <ryan.jensen@mathnotes.cc>

USER root

RUN apt-get -y update && \
  apt-get -y install \
  python3-pip \
  python3-dev

RUN pip3 install jupyter-core==4.4.0 jupyter

# Runtime Configuration
USER $MN_USER
WORKDIR $MN_HOME

CMD jupyter notebook \
  --no-browser \
  --ip=* \
  --port=8888 \
  --NotebookApp.token='' \
  --NotebookApp.password=''

# Expose Ports
EXPOSE 8888
