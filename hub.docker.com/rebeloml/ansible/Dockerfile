FROM eclipse/stack-base:ubuntu

ENV TERM=xterm

RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" | sudo tee /etc/apt/sources.list.d/ansible.list
RUN sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
RUN sudo apt-get update 
RUN sudo apt-get install ansible -y
RUN sudo apt-get install build-essential libssl-dev libffi-dev python-dev python-pip -y

WORKDIR /projects

CMD tail -f /dev/null
