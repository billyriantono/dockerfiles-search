#
# OsmBase
# Base images used by other of by images for rendering OSM maps.
#

FROM centos:7
MAINTAINER "Dirk Stichling" <mytracks@mytracks4mac.com>

# Change root password
RUN echo "root:admin" | chpasswd

# Create user gis
RUN adduser gis
RUN echo "gis:gis" | chpasswd

RUN yum -y install bzip2 unzip bzip2 psmisc && yum clean all
