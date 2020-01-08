# The electriq database migrator image
FROM electriqpower1/custom-postgres-ha:1.2.0@sha256:4589dad28cbef9a5e4de234f35283264393276414c7e6514510dafca79156f43

MAINTAINER Elctriq Power https://electriqpower.com

# Add deps
# e => error out on command error; x => print commands before executing
RUN set -ex

RUN apt-get update -yq
RUN apt-get install -yy libdbd-pg-perl  # For sqitch
RUN apt-get install -yy sqitch git

# Make data directory
RUN mkdir -p /data

# Install mysql
RUN apt-get install -yy mysql-client mysql-server

# Install gcloud tools
RUN CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" \
  && echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" \
    | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list \
  && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg \
    | apt-key add - \
  && apt-get update -qq \
  && apt-get install -yq google-cloud-sdk

# Install jq for parsing cluster data
RUN apt-get install -yy jq

# Add scripts
RUN mkdir -p /usr/local/bin/
COPY ./scripts/init /usr/local/bin/
COPY ./scripts/import /usr/local/bin/
COPY ./scripts/reset /usr/local/bin/
COPY ./scripts/migrate /usr/local/bin/
COPY ./scripts/migrator-utils /usr/local/bin/

RUN chmod +x /usr/local/bin/init
RUN chmod +x /usr/local/bin/import
RUN chmod +x /usr/local/bin/reset
RUN chmod +x /usr/local/bin/migrate
RUN chmod +x /usr/local/bin/migrator-utils

WORKDIR /data

# Run migrations
ENTRYPOINT ["/bin/sh"]
CMD ["init", "-t", "$GITHUB_TOKEN"]
CMD ["migrate", "-k", "$ENCRYPTION_KEY"]
