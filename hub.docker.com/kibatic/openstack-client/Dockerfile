FROM python:2.7

MAINTAINER Elie CHARRA <elie.charra@kibatic.com>

ENV VERSION=3.8

# Alpine-based installation
# #########################
RUN pip install --upgrade --no-cache-dir pip setuptools python-openstackclient==$VERSION python-swiftclient

# Add a volume so that a host filesystem can be mounted
# Ex. `docker run -v $PWD:/data jmcvea/openstack-client`
VOLUME ["/data"]

# Default is to start a shell.  A more common behavior would be to override
# the command when starting.
# Ex. `docker run -ti jmcvea/openstack-client openstack server list`
CMD ["/bin/sh"]

