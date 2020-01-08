FROM ubuntu:xenial
RUN apt update
RUN apt install -y software-properties-common
RUN apt-add-repository -y ppa:ansible/ansible
RUN apt update
RUN apt install -y ansible 

CMD ["bash"]