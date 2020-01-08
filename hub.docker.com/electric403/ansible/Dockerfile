FROM centos:latest

RUN yum -y update && \
    yum install -y ansible

VOLUME /ansible
WORKDIR /ansible

ENTRYPOINT ["ansible-playbook"]
CMD ["site.yml"]
