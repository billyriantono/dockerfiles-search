FROM jenkins/jenkins

USER root

RUN apt-get update && apt-get install -y python-pip && rm -rf /var/lib/apt/lists/*
RUN pip install ansible
RUN pip install "pywinrm>=0.1.1"
RUN pip install pyOpenSSL

USER jenkins
