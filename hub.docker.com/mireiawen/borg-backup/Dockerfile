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

# Install the SSH server
RUN \
	install_packages \
		"openssh-server" && \
	mkdir "/run/sshd"

# Set up the backup user
RUN \
	useradd \
		--create-home \
		--user-group \
		--shell "/bin/bash" \
		--comment "Backup User" \
		"borgbackup" && \
	ln -s "/home/borgbackup" "/backups"

# Define the directory volumes
VOLUME [ "/home/borgbackup" ]

# Set the entry point
COPY "start.sh" "/start.sh"
ENTRYPOINT [ "/bin/bash" ]
CMD [ "/start.sh" ]

# Expose the SSH port
EXPOSE 22
