FROM bitnami/minideb:stretch

MAINTAINER konmeo

RUN install_packages ca-certificates
RUN useradd -m user
RUN ln -sf /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

COPY aliases.sh /etc/profile.d/

CMD sed -n '/PRETTY_NAME/s/.*="\(.*\)"/\1/p' /etc/os-release && uname -srm
