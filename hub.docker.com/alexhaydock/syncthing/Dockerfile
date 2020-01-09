FROM syncthing/syncthing
LABEL maintainer "Alex Haydock <alex@alexhaydock.co.uk>"

# So the Syncthing container currently works very well, but cannot run
# without root privileges, as the first thing that the container executes
# is a `chmod` to account for any UID or GID that the user has passed
# to it as an environment variable.
#
# For the sake of security, I'd rather just hardcode my UID/GID and run the
# container without root or capabilities.

ENV PUID=1000 PGID=1000

# Execute the chown command that the official container would try
# and execute as part of the ENTRYPOINT. Yes, we're hard coding
# a UID/GID of 1000:1000 here, but for my purposes that's fine.
RUN chown "${PUID}:${PGID}" /var/syncthing

USER 1000
ENTRYPOINT \
    env HOME=/var/syncthing \
    /bin/syncthing \
    -home /var/syncthing/config \
    -gui-address 0.0.0.0:8384
