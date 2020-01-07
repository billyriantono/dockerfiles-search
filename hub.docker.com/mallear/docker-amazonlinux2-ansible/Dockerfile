FROM amazonlinux:2

ENV user ec2-user
ENV group ec2-user

RUN set -x \
  && yum install -y python2-pip python2-devel python2-virtualenv \
  && pip-2 install --upgrade pip \
  && python --version \
  && pip --version
RUN pip install --upgrade ansible

CMD ["/bin/bash"]
