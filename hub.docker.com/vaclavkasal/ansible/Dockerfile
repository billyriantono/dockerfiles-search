FROM ubuntu

# install ansible
RUN apt-get update
RUN apt-get install -y software-properties-common
RUN apt-add-repository ppa:ansible/ansible
RUN apt-get update
RUN apt-get install -y ansible

# install ssh
RUN apt-get install -y ssh
RUN mkdir /root/.ssh && chmod 700 /root/.ssh
RUN echo "Host *\nStrictHostKeyChecking no" >> /root/.ssh/config

# ansible vault requires vi
RUN apt-get install -y vim

# digital ocean requires dopy that is available through pip
RUN apt-get install -y python-pip
RUN pip install dopy

# mitogen
RUN wget https://networkgenomics.com/try/mitogen-0.2.9.tar.gz -O /opt/mitogen.tar.gz
RUN tar -xf /opt/mitogen.tar.gz -C /opt/
RUN rm /opt/mitogen.tar.gz
RUN mv /opt/mitogen-* /opt/mitogen/

# requirements download from git requires git module
RUN apt-get update && apt-get install -y git
RUN apt-get upgrade -y
