#    ubuntu base image new project8
FROM ubuntu:14.04

LABEL MAINTAINER <Author name and email address>

#	resynchronize the package index files
#	install the newest versions of all packages currently installed
#	packages no longer required are removed
RUN apt-get -qy update && apt-get -qy dist-upgrade && apt-get -qy autoremove 

# Create a time and date stamp of this build
RUN mkdir -p /version; \
    /usr/bin/lsb_release -a > /version/base-image-build-"$(/usr/bin/lsb_release -si):$(/usr/bin/lsb_release -sr)-$(date +"%Y-%m-%d-%H:%M:%S-%Z")"

CMD /bin/bash
