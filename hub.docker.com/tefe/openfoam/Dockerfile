FROM ubuntu:bionic
MAINTAINER "Thomas Enzinger <info@thomas-enzinger.de>"

# install software
RUN apt-get update                                        \
 && apt-get upgrade -y                                    \
 && apt-get install -y                                    \
      vim ssh sudo wget                                   \
      software-properties-common

# config os
RUN useradd --user-group --create-home --shell /bin/bash foam
RUN echo "foam ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# install openfoma
RUN sh -c "wget -O - http://dl.openfoam.org/gpg.key | apt-key add -"
RUN add-apt-repository http://dl.openfoam.org/ubuntu      \
 && apt-get update                                        \
 && apt-get install -y --no-install-recommends            \
      openfoam7

# clean up
#
RUN apt autoremove && apt clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# setup run
VOLUME ["/data"]
WORKDIR /data
USER foam
SHELL ["/bin/bash"]

COPY scripts/entrypoint.sh /opt/
ENTRYPOINT ["/opt/entrypoint.sh"]
CMD []
