FROM jenkins/jenkins:lts

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH=/opt/miniconda3/bin:$PATH

USER root


RUN apt update && apt install -y wget \
   bzip2 \
   sshpass \
   && apt clean all \
   && rm -rf /var/lib/apt/lists/* \
   && wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh \
   && chmod 775 Miniconda3-latest-Linux-x86_64.sh \
   && ./Miniconda3-latest-Linux-x86_64.sh -p /opt/miniconda3 -b \
   && rm -rf Miniconda3-latest-Linux-x86_64.sh \
   && pip install ansible \
   && conda clean --all -y

EXPOSE 8080 5000

WORKDIR "/var/jenkins_home"
