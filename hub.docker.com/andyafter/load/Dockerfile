FROM swernst/locusts:latest

MAINTAINER Andy Pan<andy.pan@grabtaxi.com>


ADD ./run.sh ./run.sh
RUN apt-get -y update && apt-get -y install  unzip 
RUN python3.6 -m pip install awscli
RUN python3.6 -m pip install --ignore-installed locustio 
ENTRYPOINT ["/bin/bash",  "run.sh"]
