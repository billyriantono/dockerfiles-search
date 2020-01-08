FROM centos:centos7

RUN yum install -y yum-utils epel-release&& yum-config-manager --disable epel
RUN yum install -y --enablerepo=epel ansible python-pip openssh openssh-clients git
RUN pip install --upgrade 'docker-py==1.2.3'

ADD entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

ADD playbooks /playbooks
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
