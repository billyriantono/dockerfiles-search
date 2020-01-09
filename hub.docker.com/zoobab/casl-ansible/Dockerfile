FROM openshift/origin-ansible:v3.11.1
USER root
RUN yum install -y --setopt=tsflags=nodocs https://repos.fedorapeople.org/repos/openstack/openstack-queens/rdo-release-queens-1.noarch.rpm && \
    yum -y install python2-pip && \
    pip install --upgrade pip && \
    yum -y install \
      python-ceilometerclient \
      python-cinderclient python-glanceclient \
      python-heatclient python-neutronclient \
      python-novaclient python-saharaclient \
      python-swiftclient python-troveclient \
      python-openstackclient python-dns \
      python2-pyOpenSSL python-shade \
      python2-boto3 && \
      yum clean all && \
      rm -rf /var/cache/yum && \
    rpm -e --nodeps python-ipaddress PyYAML && \
    pip install --upgrade \
      "Paste>=2.0.2" \
      "eventlet!=0.18.3,!=0.20.1,<0.21.0,>=0.18.2" \
      openstacksdk
COPY root /
RUN /usr/local/bin/user_setup_casl
USER root
ENTRYPOINT [ "/usr/local/bin/entrypoint_casl" ]
CMD [ "/usr/local/bin/run" ]
