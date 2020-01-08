FROM shawnyan/centos
LABEL Description="CentOS7+Ansible2.8"

# Install Deps
RUN yum install -y openssh openssh-clients openssh-server \
    PyYAML libtomcrypt libtommath libyaml python-babel \
    python-backports python-backports-ssl_match_hostname python-cffi \
    python-enum34 python-httplib2 python-idna python-ipaddress \
    python-jinja2 python-keyczar python-markupsafe python-paramiko \
    python-ply python-pycparser python-setuptools python-six \
    python2-crypto python2-cryptography python2-jmespath python2-pyasn1 \
    sshpass python2-packaging python-docutils python-devel

# Install Ansible
COPY ansible-2.8.0.rpm /ansible-2.8.0.rpm
RUN yum install -y /ansible-2.8.0.rpm && \
    /bin/rm /ansible-2.8.0.rpm && \
    /bin/echo -e "[local]\nlocalhost ansible_connection=local" >> /etc/ansible/hosts && \
    /bin/echo -e '[dbservers]\n172.5.0.10[1:3]' >> /etc/ansible/hosts && \
    grep -v '^#\|^$' /etc/ansible/hosts

# SSH Config
RUN ssh-keygen -q -t rsa -N '' -f /root/.ssh/id_rsa && \
    cp /root/.ssh/id_rsa.pub /root/.ssh/authorized_keys && \
    for key in /etc/ssh/ssh_host_*_key.pub; do echo "localhost $(cat ${key})" >> /root/.ssh/known_hosts; done
