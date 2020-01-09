#
# clouberry-backup Dockerfile
#
# https://github.com/jlesage/docker-cloudberry-backup
#

# Pull base image.
FROM jlesage/baseimage-gui:alpine-3.8-glibc-v3.5.1

# Define software download URLs.
ARG CLOUDBERRYBACKUP_URL=https://github.com/avandeweghe/docker-cloudberry-backup/raw/master/ubuntu14_CloudBerryLab_CloudBerryBackup_v2.8.0.35_20190223034507_c528593.deb

# Define working directory.
WORKDIR /tmp

# Install CloudBerry Backup.
RUN \
    # Install packages needed by the build.
    add-pkg --virtual build-dependencies dpkg tar curl bash && \

    # Download the CloudBerry Backup package.
    echo "Downloading CloudBerry Backup package..." && \
    curl -# -L -o cloudberry-backup.deb ${CLOUDBERRYBACKUP_URL} && \

    # Extract the CloudBerry Backup package.
    dpkg-deb --raw-extract cloudberry-backup.deb cbbout && \
    mv cbbout/opt/* /opt/ && \

    # Install CloudBerry Backup.
    sed-patch '/^#!\/bin\/bash/ a\\nfunction service {\n    :\n}\nfunction update-rc.d {\n    :\n}' cbbout/DEBIAN/postinst && \
    ./cbbout/DEBIAN/postinst && \

    # Modify installed scripts to use sh instead of bash.
    find /opt/local/CloudBerry\ Backup/bin/ -type f -exec sed-patch 's/^#!\/bin\/bash/#!\/bin\/sh/' {} \; && \

    # Save default configuration.
    mkdir -p /defaults && \
    mv /opt/local/"CloudBerry Backup"/etc /defaults/cbb_etc && \

    # Setup symbolic links for stuff that need to be outside the container.
    ln -s /config/etc /opt/local/"CloudBerry Backup"/etc && \
    rm -r /opt/local/"CloudBerry Backup"/logs && \
    ln -s /config/logs /opt/local/"CloudBerry Backup"/logs && \
    ln -s /config/HID /opt/local/"CloudBerry Backup"/share/HID && \

    # Fix PAM authentication for web interface.
    ln -s base-auth /etc/pam.d/common-auth && \

    # Maximize only the main/initial window.
    sed-patch 's/<application type="normal">/<application type="normal" title="CloudBerry Backup">/' \
        /etc/xdg/openbox/rc.xml && \

    # Cleanup.
    del-pkg build-dependencies && \
    rm -rf /tmp/*

# Install dependencies.
RUN \
    add-pkg \
        ca-certificates \
        mkpasswd

# Generate and install favicons.
ARG APP_ICON_URL=https://github.com/jlesage/docker-templates/raw/master/jlesage/images/cloudberry-backup-icon.png
RUN install_app_icon.sh "$APP_ICON_URL"

# Add files.
COPY rootfs/ /

# Set environment variables.
ENV APP_NAME="CloudBerry Backup" \
    CBB_WEB_INTERFACE_USER="" \
    CBB_WEB_INTERFACE_PASSWORD=""

# Define mountable directories.
VOLUME ["/config"]
VOLUME ["/storage"]

# Expose ports.
#   - 43210: CloudBerry Backup web interface (HTTP).
#   - 43211: CloudBerry Backup web interface (HTTPs).
EXPOSE 43210 43211
