FROM debian:stretch AS outer
RUN apt-get update && apt-get install -y debootstrap
RUN debootstrap --foreign stretch /rootfs

# run the second stage, using Docker for the "chroot"ing
FROM scratch AS rootfs
COPY --from=outer /rootfs /

# prevent debootstrap from mucking with /proc (which Docker already preps for us)
RUN sed -i 's/setup_proc/echo skipping setup_proc/' /debootstrap/suite-script
RUN /debootstrap/debootstrap --second-stage

# tell 'man' not to cache man pages, this is extra cruft and we don't want to keep it in the image
RUN test ! -f /etc/manpath.config || sed -i 's/^#NOCACHE/NOCACHE/' /etc/manpath.config
RUN rm -rf /var/cache/man

# add stretch main repos and update
RUN echo 'deb http://deb.debian.org/debian-security/ stretch/updates main' >/etc/apt/sources.list.d/stretch-security.list
RUN echo 'deb http://deb.debian.org/debian stretch-updates main' >/etc/apt/sources.list.d/stretch-updates.list
RUN apt-get update && apt-get -y upgrade

# some useful packages in a base machine image
RUN apt-get update && apt-get install --no-install-recommends -y openssh-server lsb-release sudo ifenslave curl mdadm jq apt-transport-https tcpdump nano vim jq python python-yaml

# add stretch backports and install latest kernel from backports
RUN echo 'deb http://ftp.debian.org/debian stretch-backports main' >/etc/apt/sources.list.d/stretch-backports.list
RUN apt-get update && apt-get -t stretch-backports install -y linux-image-amd64

# clean up other files left around by debootstrap
RUN rm -rf \
	/var/log/dpkg.log \
	/var/log/bootstrap.log \
	/var/log/alternatives.log \
	/var/cache/ldconfig/aux-cache \
	;

# remove large files left in the image
RUN apt-get autoremove -y --purge
RUN apt-get clean

# finally, remove all layers, squash into the output rootfs
FROM scratch
COPY --from=rootfs / /
