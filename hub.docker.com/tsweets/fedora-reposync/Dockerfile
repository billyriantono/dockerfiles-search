FROM fedora:29
LABEL maintainer="tony.sweets@gmail.com"
RUN dnf install -y dnf-utils createrepo
 
ADD sync.sh /root
ENTRYPOINT ["/bin/bash", "/root/sync.sh"]
