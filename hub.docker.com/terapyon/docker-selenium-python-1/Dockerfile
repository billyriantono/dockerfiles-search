FROM selenium/standalone-chrome
MAINTAINER "Manabu TERADA" <terada@cmscom.jp>
RUN sudo locale-gen en_US.UTF-8  
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8
RUN sudo apt-get update
RUN sudo apt-get install -y build-essential
RUN sudo apt-get install -y libpq-dev
RUN sudo apt-get install -y postgresql-server-dev-all
RUN sudo apt-get install -y software-properties-common
#RUN sudo apt-get install -y python-software-properties
RUN sudo add-apt-repository ppa:fkrull/deadsnakes
RUN sudo apt-get update
RUN sudo apt-get install -y python3.5
RUN sudo apt-get install -y python3.5-dev
RUN sudo wget https://bootstrap.pypa.io/get-pip.py
RUN sudo python3.5 get-pip.py
RUN sudo pip install virtualenv
#CMD ["/bin/bash"]
