FROM ubuntu:18.04

RUN apt-get update 

RUN apt-get upgrade -y

RUN apt-get install htop vim wget curl openjdk-8-jdk python3-pip  -y

# nodejs 8
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs git

# building the repo
RUN git clone https://github.com/matheusmota/jupyterlab-docker
RUN pip3 install -r jupyterlab-docker/binder/requirements.txt
RUN sh jupyterlab-docker/binder/postBuild

ENV LANG=C.UTF-8

# Expose Jupyter port & cmd
# Add Tini. Tini operates as a process subreaper for jupyter. This prevents kernel crashes.
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

EXPOSE 8888
CMD ["jupyter", "lab", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root", "--NotebookApp.token=''", "--notebook-dir=/opt/app/data"]
