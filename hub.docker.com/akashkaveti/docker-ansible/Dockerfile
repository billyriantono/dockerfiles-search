FROM ubuntu
RUN apt-get update
RUN apt-get install software-properties-common -y
RUN apt-add-repository ppa:ansible/ansible -y
RUN apt-get update
RUN apt-get install ansible -y

CMD /bin/bash
