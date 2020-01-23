# Pull base image.
FROM phusion/baseimage:0.11

# Define s6 overlay related variables.
ARG S6_OVERLAY_ARCH=amd64
ARG S6_OVERLAY_VERSION=1.21.8.0
ARG S6_OVERLAY_URL=https://github.com/just-containers/s6-overlay/releases/download/v${S6_OVERLAY_VERSION}/s6-overlay-${S6_OVERLAY_ARCH}.tar.gz

# Variables needed for package installation via APT.
ARG DEBIAN_FRONTEND=noninteractive
ARG TERM=xterm

# Define working directory.
WORKDIR /tmp

# Copy files
COPY rootfs/ /tmp/rootfs/

RUN \
	chmod -R +x /tmp/rootfs && \
	cp -R /tmp/rootfs/* / && \
	# Timezone
	add-pkg tzdata && \
	# Install s6 overlay.
	add-pkg --virtual build-dependencies curl ca-certificates patch && \
	echo "Downloading s6-overlay..." && \
	curl -# -L -o s6-overlay.tar.gz ${S6_OVERLAY_URL} && \
	echo "Installing s6-overlay..." && \
	# Workaround for some distro where '/bin' being a symlink to '/usr/bin':
	# extract the tarball in two steps.
	if [ -L /bin ]; then \
		tar xzf s6-overlay.tar.gz -C / --exclude="./bin" && \
		tar xzf /tmp/s6-overlay.tar.gz -C /usr ./bin; \
	else \
		tar xzf s6-overlay.tar.gz -C /; \
	fi && \
	echo "Patching s6-overlay..." && \
	curl -# -L https://github.com/jlesage/s6-overlay/commit/d151c41.patch | patch -d / -p3 && \
    chmod +x \
		/etc/s6/services/.s6-svscan/SIGHUP \
		/etc/s6/services/.s6-svscan/SIGINT \
		/etc/s6/services/.s6-svscan/SIGQUIT \
		/etc/s6/services/.s6-svscan/SIGTERM \
		/usr/bin/sv-getdeps \
		&& \
	# Cleanup
	del-pkg build-dependencies && \
	rm -rf /tmp/* /tmp/.[!.]* && \
	# Make sure VERSION_CODENAME is set in /etc/os-release.
	if ! grep -q "^VERSION_CODENAME=" /etc/os-release; then \
		add-pkg lsb-release && \
		echo "VERSION_CODENAME=$(lsb_release -c -s)" >> /etc/os-release && \
		del-pkg lsb-release; \
	fi && \
	# Save some defaults.
	mkdir /defaults && \
	cp /etc/passwd /defaults/ && \
	cp /etc/group /defaults/ && \
	cp /etc/shadow /defaults/

# Set environment variables.
ENV S6_BEHAVIOUR_IF_STAGE2_FAILS=3 \
	S6_SERVICE_DEPS=1 \
	USER_ID=1000 \
	GROUP_ID=1000 \
	APP_NAME=DockerApp \
	APP_USER=app \
	XDG_DATA_HOME=/config/xdg/data \
	XDG_CONFIG_HOME=/config/xdg/config \
	XDG_CACHE_HOME=/config/xdg/cache \
	XDG_RUNTIME_DIR=/tmp/run/user/app

# Define mountable directories.
VOLUME ["/config"]

# Define default command.
# Use S6 overlay init system.
CMD ["/init"]
