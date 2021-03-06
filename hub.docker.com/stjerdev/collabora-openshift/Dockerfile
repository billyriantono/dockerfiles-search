FROM openshift/base-centos7

# Install Collabora, libmapuid and dumb-init
RUN yum -y --setopt=tsflags=nodocs install wget openssl && \
    wget https://www.collaboraoffice.com/repos/CollaboraOnline/CODE-centos7/repodata/repomd.xml.key && \
    rpm --import repomd.xml.key && \
    yum-config-manager --add-repo https://www.collaboraoffice.com/repos/CollaboraOnline/CODE-centos7 && \
    yum -y --setopt=tsflags=nodocs --nogpgcheck install loolwsd CODE-brand && \
    # dumb-init
    wget -O /usr/local/sbin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64 && \
    chmod +x /usr/local/sbin/dumb-init && \
    # libmapuid
    curl https://raw.githubusercontent.com/appuio/libmapuid/master/lib/libmapuid.so -o /usr/local/lib/libmapuid.so && \
    chmod 755 /usr/local/lib/libmapuid.so && \
    echo "/usr/local/lib/libmapuid.so" > /etc/ld.so.preload

# Setup directories and permissions - prepare for libmapuid
RUN mkdir /home/lool && \
    directories="/home/lool /etc/loolwsd /var/cache/loolwsd /opt/lool" && \
    chgrp -R 0 $directories && \
    chmod -R g=u $directories

ADD entrypoint.sh /
COPY loolwsd.xml /etc/loolwsd/loolwsd.xml

USER 1001
EXPOSE 9980

ENTRYPOINT ["dumb-init", "/entrypoint.sh"]
CMD ["loolwsd"]
