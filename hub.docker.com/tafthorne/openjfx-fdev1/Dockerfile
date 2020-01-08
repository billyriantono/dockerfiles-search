# GNU GCC, Clang & other Libraries

FROM tafthorne/fdev1
LABEL \
 Description="Basic GNU gcc & OpenJFX Debian environment with a number of libraries configured" \
 MAINTAINER="Thomas Thorne <TafThorne@GoogleMail.com>"
USER root
RUN apt-get -y update && \
  apt-get -y install \
    openjfx
USER builder

