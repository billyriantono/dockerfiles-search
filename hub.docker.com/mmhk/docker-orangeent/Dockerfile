FROM "bitnami/minideb:stretch"

MAINTAINER "Mira Liikanen <mir@mireiawen.net>"

# Write the backports list file for current codename
RUN \
	echo "deb http://ftp.debian.org/debian stretch-backports main" \
		>"/etc/apt/sources.list.d/backports.list" 

# Install the Borg backup itself
RUN \
	install_packages \
		-t "stretch-backports" \
		"borgbackup"

# Install SSH for remote jobs
RUN \
	install_packages \
		"openssh-client"

# Set the entry point
ENTRYPOINT [ "/usr/bin/borg" ]
CMD [ "--help" ]
