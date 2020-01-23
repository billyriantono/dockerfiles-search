FROM kalilinux/kali-rolling
MAINTAINER chasepd <1214246+chasepd@users.noreply.github.com>

#environment-variables for non-interactive shell:
ENV DEBIAN_FRONTEND noninteractive

#install updates and the metasploit package, and update metasploit to get the latest updates and modules:
RUN apt-get update \
  && apt-get upgrade -y\
  && apt-get -y install metasploit-framework \
  && msfupdate

ENTRYPOINT ["/usr/bin/msfconsole"]
