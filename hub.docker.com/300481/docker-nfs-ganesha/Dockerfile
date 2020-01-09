# the consolidator for s6-overlay and config file and start script
FROM ubuntu:bionic AS consolidator

RUN apt-get update && \
    apt-get install -y wget ca-certificates && \
    mkdir /files && \
    wget https://github.com/just-containers/s6-overlay/releases/download/v1.22.1.0/s6-overlay-amd64.tar.gz && \
    tar xvzf s6-overlay-amd64.tar.gz -C /files

# copy files
COPY files/ /files/

# now the application container
FROM ubuntu:bionic
LABEL maintainer="Dennis Riemenschneider <30048@300481.de>"

LABEL org.label-schema.name="300481/docker-nfs-ganesha"
LABEL org.label-schema.docker.cmd="docker run -d --privileged -e CRYPT_KEY_URL --cap-add SYS_ADMIN --cap-add DAC_READ_SEARCH --cap-add MKNOD --name nfs -p 2049:2049 -v /data/path:/mnt/data -v /dev:/dev 300481/docker-nfs-ganesha"
LABEL org.label-schema.vcs-url="https://github.com/300481/docker-nfs-ganesha"

# install prerequisites
RUN DEBIAN_FRONTEND=noninteractive \
 && apt-get -y update \
 && apt-get -y install software-properties-common \
 && add-apt-repository -y ppa:nfs-ganesha/libntirpc-3.0 \
 && add-apt-repository -y ppa:nfs-ganesha/nfs-ganesha-3.0 \
 && add-apt-repository -y ppa:gluster/glusterfs-6 \
 && apt-get -y update \
 && apt-get install -yq --no-install-recommends nfs-ganesha-vfs netbase dbus glusterfs-common cryptsetup curl ca-certificates \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 && mkdir -p /run/rpcbind /export /var/run/dbus /mnt/data \
 && touch /run/rpcbind/rpcbind.xdr /run/rpcbind/portmap.xdr \
 && chmod 755 /run/rpcbind/* \
 && chown messagebus:messagebus /var/run/dbus

COPY --from=consolidator /files/ /

# NFS port
EXPOSE 2049

# run init
ENTRYPOINT ["/init"]
