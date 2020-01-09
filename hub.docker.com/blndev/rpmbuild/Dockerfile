FROM centos:7
LABEL maintainer="blndev"

RUN yum install epel-release -y
RUN yum install -y \
	gcc \
	make \
	python-devel \
    python-setuptools \
    python-pip \
    pytest \
    python2-pytest-cov \
	rpm-build \
	rpm-sign && yum clean all

#RUN pip install ....

#VOLUME [ "/tmp/rpm" ]
WORKDIR /tmp/rpm

CMD ["/bin/bash"]
