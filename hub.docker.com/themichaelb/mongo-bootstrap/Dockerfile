FROM mongo:3.6

COPY --chown=999:999 scripts/init.sh /init.sh
RUN set -ex; \
	\
	apt-get update; \
	apt-get install -y --no-install-recommends \
		wget ed curl \
	; \
	rm -rf /var/lib/apt/lists/*; \
    wget -qO /usr/local/bin/peer-finder http://storage.googleapis.com/kubernetes-release/pets/peer-finder; \
    chmod -c +x /init.sh; \
    chmod -c 755 /usr/local/bin/peer-finder; \
    apt-get purge -y --auto-remove wget 

ENTRYPOINT []