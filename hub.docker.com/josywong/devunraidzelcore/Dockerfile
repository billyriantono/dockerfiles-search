# Pull base image.
FROM angelics/unraid-docker-baseimage-gui:phusion-0.11

# Define working directory.
WORKDIR /tmp

# Add files
COPY rootfs/ /tmp/rootfs/

RUN \
	chmod -R +x /tmp/rootfs/ && \
	cp -R /tmp/rootfs/* / && \
	echo "add zelcore dependencies..." && \
	add-pkg \
		gconf2 \
		gconf-service \
		libnotify4 \
		libappindicator1 \
		libnss3 \
		libxss1 \
		libgtk-3-0 \
		libasound2 \
		wget \
		ca-certificates \
		&& \
	apt-get purge --auto-remove gcc-7-base -y && \
	rm -rf /tmp/* /tmp/.[!.]* && \
	# Generate and install favicons.
    APP_ICON_URL=https://raw.githubusercontent.com/angelics/unraid-docker-zelcore-wallet/master/favicon.png && \
    install_app_icon.sh "$APP_ICON_URL"

# Set environment variables.
ENV	APP_NAME="ZelcoreWalletGUI"

# Define mountable directories.
VOLUME ["/config"]
VOLUME ["/storage"]