FROM openshift/jenkins-2-centos7:latest

USER 0
RUN yum install -y bzip2
RUN curl -o miniconda.sh https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN bash miniconda.sh -b -p /opt/miniconda

RUN ln -s /opt/miniconda/bin/python /usr/local/bin/python
RUN ln -s /opt/miniconda/bin/pip /usr/local/bin/pip
RUN ln -s /opt/miniconda/bin/conda /usr/local/bin/conda

USER 1001
