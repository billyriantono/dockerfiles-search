FROM gethec/dockerbase:0.0.3

# Install updates and required packages
RUN apt-get update && \
	apt-get install -y --no-install-recommends \
		openssh-server \
		fail2ban \
		iptables \
		libpam-google-authenticator && \
# Clean up after install
	rm -rf \
		/tmp/* \
		/var/lib/apt/lists/* \
		/var/tmp/* \
# Clear out automatically generated keys so each container is unique
		/etc/ssh/ssh_host*

# Set default container options
ENV ENABLEKEY="On" \
	ENABLEPASS="Off" \
	ENABLE2FA="Off" \
	ENABLESFTP="Off" \
# Set paths used by container
	HOME_DIR="/home/docker" \
	F2B_CONF="/config/fail2ban" \
	SSHD_CONF="/config/sshd" \
	SSHD_KEYS="/config/keys"
#Set variables that require on previous ones
ENV SSHD_LOG="$SSHD_CONF/logs" \
	SSHD_SKEYS="$SSHD_CONF/serverkeys" \
	F2B_LOG="$F2B_CONF/logs"

# Final prep
COPY root/ /
EXPOSE 22
VOLUME /config

# Initiate
ENTRYPOINT ["/init"]
