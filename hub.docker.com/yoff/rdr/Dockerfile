FROM centos:latest
ENV PATH="${PATH}:/obsr/bin:/obsr/check:/bootstrap" \
    APP=rdr \
    APP_HOME=/rdr \
    TEMPLATES=/bootstrap/templates \
    UID=400 \
    GID=400
WORKDIR ${APP_HOME}


# Download the *nix installer directly from ahsay.com
#ADD https://ahsay-dn.ahsay.com/v6/obsr/62900/rdr-nix.tar.gz ./
#RUN tar xzf rdr-nix.tar.gz \
#    && rm -f rdr-nix.tar.gz


# Alternative to the above, this extraction is much lighter.
# See .gitignore for the full list of what is excluded.
COPY ${APP}/ ./


# 'bootstrap' contains docker-entrypoint.sh (SIGTERM receiver),
# templates, configuration tools, pseudo ifconfig, etc
COPY bootstrap/ /bootstrap


RUN \
#
#
# Symlink pseudo ifconfig.
  ln -sf /bootstrap/bin/ifconfig /usr/bin/ifconfig && \
#
#
# Ensure conf and policy paths exist
#     (critical for downstream java7 image)
  mkdir -p "conf" && \
#
#
# Create the limited user and group that will be used to run APP
  groupadd --gid ${GID} ahsay && \
  useradd --uid ${UID} --gid 400 --no-create-home ahsay  && \
#
#
# Change owner and group to ahsay user
  chown -R ahsay:ahsay "." "/bootstrap"


# De-escalate from root
USER ahsay


ENTRYPOINT ["/bootstrap/docker-entrypoint.sh"]
