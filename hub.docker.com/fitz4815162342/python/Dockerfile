FROM python:3.6

RUN apt-get update && apt-get install -y sudo gcc libxml2-dev libxslt1-dev zlib1g-dev libffi-dev libssl-dev 

RUN pip install pysftp==0.2.8 ecdsa paramiko numpy pandas scipy scikit-learn seaborn

RUN adduser --disabled-password --gecos '' me
RUN adduser me sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER me

WORKDIR /home/me

EXPOSE 22
