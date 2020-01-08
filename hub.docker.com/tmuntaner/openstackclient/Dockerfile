FROM opensuse/leap:15

RUN zypper --non-interactive up && \
    zypper --non-interactive install --no-recommend python3-openstackclient

RUN mkdir /etc/openstack

ENTRYPOINT ["/bin/bash"]
