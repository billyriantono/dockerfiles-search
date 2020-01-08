FROM vflong/sshd
MAINTAINER feilong <weifeilong2013@gmail.com>

RUN yum clean all && \
    yum -y install ansible && \
    rm -rf /var/cache/yum
RUN mkdir -p /etc/ansible/
RUN echo -e '[local]\nlocalhost' > /etc/ansible/hosts
RUN echo 'export ANSIBLE_HOST_KEY_CHECKING=false' > /etc/profile.d/ansible.sh

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
