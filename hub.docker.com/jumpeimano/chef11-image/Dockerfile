FROM busybox

ARG CHANNEL=stable
ARG VERSION=11.10

RUN wget "https://packages.chef.io/files/stable/chef-server/11.1.7/el/6/chef-server-11.1.7-1.el6.x86_64.rpm" -O /tmp/chef-client.rpm && \
    rpm2cpio /tmp/chef-client.rpm | cpio -idmv && \
    rm -rf /tmp/chef-client.rpm

VOLUME [ "/opt/chef" ]
