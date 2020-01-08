FROM jenkinsci/ssh-slave

USER root

WORKDIR /opt
ADD tasks.py /opt/tasks.py
RUN apt-get update && apt-get install -y \
python-dev \
python-git \
wget && \
wget https://bootstrap.pypa.io/get-pip.py --no-check-certificate 

RUN python get-pip.py && pip install --upgrade pip && pip install virtualenv && pip install invoke && inv install && apt-get autoclean && rm -rf /var/lib/apt/lists/* 

USER ${user}

EXPOSE 22
ENTRYPOINT ["setup-sshd"]
