FROM debian:stretch as BUILDER
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get -qqy update \
 && apt-get -qqy install git build-essential \
 && git clone https://github.com/dark/dropbox-filesystem-fix.git \
 && cd dropbox-filesystem-fix \
 && make \
 && mkdir -p /opt/dropbox-filesystem-fix \
 && cp libdropbox_fs_fix.so /opt/dropbox-filesystem-fix/ 

#MAINTAINER Jan Broer <janeczku@yahoo.de>
FROM debian:stretch-slim
ENV DEBIAN_FRONTEND noninteractive

# Following 'How do I add or remove Dropbox from my Linux repository?' - https://www.dropbox.com/en/help/246
RUN apt-get -qqy update \
 && apt-get -qqy install --no-install-recommends ca-certificates curl python3-gpg \
 # Perform image clean up.
 && apt-get -qqy autoclean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 # Create service account and set permissions.
 && groupadd dropbox \
 && useradd -m -d /dbox -c "Dropbox Daemon Account" -s /usr/sbin/nologin -g dropbox dropbox \
 && curl -o /usr/bin/dropbox -L https://www.dropbox.com/download?dl=packages/dropbox.py \
 && chmod +x /usr/bin/dropbox \
 && mkdir -p /dbox/.dropbox /dbox/.dropbox-dist /dbox/Dropbox /dbox/base \
 && cd /dbox \
 && curl -# -L "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf - \
 && echo y | dropbox update \
 && mkdir -p /opt/dropbox \
 # Prevent dropbox to overwrite its binary
 && mv /dbox/.dropbox-dist/dropbox-lnx* /opt/dropbox/ \
 && mv /dbox/.dropbox-dist/dropboxd /opt/dropbox/ \
 && mv /dbox/.dropbox-dist/VERSION /opt/dropbox/ \
 && rm -rf /dbox/.dropbox-dist \
 && install -dm0 /dbox/.dropbox-dist \
 # Prevent dropbox to write update files
 && chmod u-w /dbox \
 && chmod o-w /tmp \
 && chmod g-w /tmp \
 # Prepare for command line wrapper
 && mv /usr/bin/dropbox /usr/bin/dropbox-cli


COPY --from=BUILDER /opt/dropbox-filesystem-fix /opt/dropbox-filesystem-fix
# Dropbox is weird: it insists on downloading its binaries itself via 'dropbox
# start -i'. So we switch to 'dropbox' user temporarily and let it do its thing.
USER dropbox
RUN mkdir -p /dbox/.dropbox /dbox/.dropbox-dist /dbox/Dropbox /dbox/base 


# Switch back to root, since the run script needs root privs to chmod to the user's preferrred UID
USER root

# Dropbox has the nasty tendency to update itself without asking. In the processs it fills the
# file system over time with rather large files written to /dbox and /tmp. The auto-update routine
# also tries to restart the dockerd process (PID 1) which causes the container to be terminated.
 
# Install init script and dropbox command line wrapper
COPY run /root/
COPY dropbox /usr/bin/dropbox

WORKDIR /dbox/Dropbox
EXPOSE 17500
VOLUME ["/dbox/.dropbox", "/dbox/Dropbox"]
ENTRYPOINT ["/root/run"]

