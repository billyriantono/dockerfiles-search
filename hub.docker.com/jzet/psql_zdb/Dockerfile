# Postgres v9.5 with ZomboDB v5.6.4-1.0.1

FROM postgres:9.5

# Define ENV with most recent Version
ENV ZOMBODB_VER 5.6.4-1.0.1

# Install wget
RUN set -x && \
	apt-get update && apt-get install -y --no-install-recommends ca-certificates wget && rm -rf /var/lib/apt/lists/* && \
    apt-get update -y -qq --fix-missing

# Download zomboDB
RUN set -x && \
  cd / && \
  mkdir zombodb && \
  cd zombodb && \
  wget https://www.zombodb.com/releases/v${ZOMBODB_VER}/zombodb_jessie_pg95-${ZOMBODB_VER}_amd64.deb

# Install zomboDB
RUN \
  cd /zombodb && \
  dpkg -i zombodb_jessie_pg95-${ZOMBODB_VER}_amd64.deb

COPY zombodb-entrypoint.sh /

RUN chmod +x /zombodb-entrypoint.sh

ENTRYPOINT ["/zombodb-entrypoint.sh"]

CMD ["postgres"]