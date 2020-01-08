FROM phusion/baseimage

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]


# Install Ansible and a few other utilities
RUN echo "starting install" \
 && apt-get update -qq \
 && apt-get install -qqy --no-install-recommends ca-certificates curl screen wget git software-properties-common python-software-properties \
 && apt-add-repository ppa:ansible/ansible \
 && apt-get update -qq \
 && apt-get install -qqy ansible

 # Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
