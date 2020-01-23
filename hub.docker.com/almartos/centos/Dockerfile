FROM scratch
ADD centos-7-docker.tar.xz /

LABEL org.label-schema.schema-version="1.0" \
    org.label-schema.name="CentOS Base Image" \
    org.label-schema.vendor="CentOS" \
    org.label-schema.license="GPLv2" \
    org.label-schema.build-date="20181205"
RUN yum -y update
RUN yum -y upgrade
RUN yum -y install git
RUN yum -y install vim
RUN yum -y install centos-release-scl
RUN yum -y install rh-python36
RUN echo "source scl_source enable rh-python36" >> /etc/bashrc
RUN curl https://bootstrap.pypa.io/get-pip.py | python
RUN git clone https://github.com/instabot-py/instabot.py.git
WORKDIR /instabot.py
RUN /opt/rh/rh-python36/root/usr/bin/pip3 install -e .
#COPY . .
CMD ["/bin/bash"]
#CMD ["python", "example.py"]
