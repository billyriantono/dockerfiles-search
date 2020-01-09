# Cloud9 server
# A lot inspired by https://hub.docker.com/r/gai00/cloud9/~/dockerfile/
#                   https://hub.docker.com/r/kdelfour/cloud9-docker/~/dockerfile/
#
# Notes: 
# This dockerfile may not work on RPi you can find more info on how make it work on this issue:
# https://github.com/sapk/dockerfiles/issues/40

FROM mstev0du/cloud9-ide
LABEL maintainer="Jedidiah Carlson <jed.e.carlson@gmail.com>"

USER root

RUN apt-get update && apt-get upgrade -y \
 && apt-get install -y python3-enchant wget \
 && wget -O get-pip.py 'https://bootstrap.pypa.io/get-pip.py' \
 && python3 get-pip.py \
    --disable-pip-version-check \
    --no-cache-dir \
 && pip install --no-cache-dir flake8 flake8-docstrings pylint pyenchant yapf virtualenv

# ------------------------------------------------------------------------------
# Clean up APT when done
# ------------------------------------------------------------------------------
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
# ------------------------------------------------------------------------------
# allow binding for and application running for non-root
# ------------------------------------------------------------------------------
RUN setcap 'cap_net_bind_service=+ep' /usr/bin/node
RUN chown -R c9user:c9user /cloud9
RUN chown -R c9user:c9user /c9files
RUN chown -R c9user:c9user /workspace
RUN npm i --production
# ------------------------------------------------------------------------------
# Expose ports.
# ------------------------------------------------------------------------------
EXPOSE 80
EXPOSE 3000
# ------------------------------------------------------------------------------
# Startup commands and entrypoint
# ------------------------------------------------------------------------------
ENTRYPOINT ["fixuid"]
CMD ["/bin/sh", "-c", "/usr/bin/node /cloud9/server.js --listen 0.0.0.0 --port 80 -w /workspace"]

USER c9user:c9user

