FROM mesaguy/fedora-27-kitchen-base-x86_64:latest

# Python symlink for ansible
RUN ln -s /usr/bin/python3 /usr/bin/python && \
# Purge logs
rm -rf /var/log/* /var/run/log/journal

# Image metadata
LABEL org.label-schema.vendor="Mesaguy" \
      org.label-schema.name="Fedora Linux 27 kitchen-ansible" \
      org.label-schema.description="Image boots Fedora Linux 27 via systemd configured for kitchen ansible testing" \
      com.mesaguy.operatingsystem.eol="false"
