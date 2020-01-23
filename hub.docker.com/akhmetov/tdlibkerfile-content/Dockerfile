FROM fedora
MAINTAINER Abhijeet Kasurde (akasurde@redhat.com)
RUN dnf install -y rpm rpm-build python-pip gcc wget git libffi-devel redhat-rpm-config python-devel\
    openssl-devel && dnf clean all
RUN ssh-keygen -f /root/.ssh/id_rsa -t rsa -N ''
RUN printf "Host *\n    StrictHostKeyChecking no" > /root/.ssh/config
RUN pip install pytest pyvmomi
