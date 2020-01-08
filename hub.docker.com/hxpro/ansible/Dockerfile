FROM centos
RUN yum install -y epel-release \
 && yum install -y \
        openssh-clients \
        docker-client \
        python2-pip \
 && yum clean all
RUN pip install --no-cache-dir pip --upgrade \
 && pip install --no-cache-dir ansible docker-py
ENV SSH_AUTH_SOCK=/root/ssh-agent
VOLUME ["/ansible/", "/var/run/docker.sock", "/root/ssh-agent"]
WORKDIR /ansible/
