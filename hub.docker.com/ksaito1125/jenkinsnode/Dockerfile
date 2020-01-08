FROM jenkinsci/jnlp-slave

USER root
RUN apt-get update -y && apt-get install -y \
    sudo \
    python-pip \
    ansible \
    make \
 && apt-get -y autoremove && rm -rf /var/lib/apt/lists/*
RUN pip install awscli
RUN usermod -aG sudo jenkins \
 && echo "jenkins ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER jenkins
