FROM ubuntu:14.04
MAINTAINER Mark Fernandes mark.fernandes@ifr.ac.uk
#MAINTAINER Mark Dunning<mark.dunning@cruk.cam.ac.uk>

USER root
RUN apt-get -qq update && apt-get upgrade -y && apt-get install -y software-properties-common python-pip ipython ipython-notebook git
RUN git clone https://github.com/pycam/python-intro.git

EXPOSE 8888
ENV USE_HTTP 0

WORKDIR python-intro/
RUN ipython notebook --no-browser --port 8888 --ip=* Introduction_to_python_session_1.ipynb &

#-------------------------------------
#

#RUN mkdir /scripts
#ADD runner.sh /scripts/runner.sh
#RUN chmod +x /scripts/runner.sh
#Launch the notebook server
#RUN ipython notebook --no-browser --port=8888 --ip=0.0.0.0 &
#EXPOSE :8888
#CMD ["/scripts/runner.sh"]
