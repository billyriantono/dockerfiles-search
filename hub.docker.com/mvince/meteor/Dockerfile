FROM centos:7
RUN yum install -y which bsdtar

RUN ln -sf $(which bsdtar) $(which tar)
RUN curl https://install.meteor.com/ | sh

ENV METEOR_ALLOW_SUPERUSER 1

ENTRYPOINT ["meteor"]