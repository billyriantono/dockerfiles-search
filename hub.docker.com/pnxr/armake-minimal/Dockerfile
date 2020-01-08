FROM debian:stretch-slim
MAINTAINER pnxr@regxr.eu

#environment
ARG ARMAKE_MIRROR="https://github.com/KoffeinFlummi/armake.git"
ARG ARMAKE_DEPENDENCIES="libssl1.1"
ARG BUILD_DEPENDENCIES="libssl-dev build-essential bison flex git ca-certificates"
ARG DEBIAN_FRONTEND=noninteractive
ARG USER=armake

#update base system, install all deps, download armake & install, remove build deps, cleanup image
RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends ${BUILD_DEPENDENCIES} ${ARMAKE_DEPENDENCIES}; \
	useradd -d /home/${USER} -ms /bin/bash ${USER} && cd /home/${USER}; \
	git clone ${ARMAKE_MIRROR} armake_installer && cd armake_installer && make && make install; \
	mkdir -p /data && cd /data; \
	chown -R ${USER}:${USER} /home/${USER} /data; \
	apt-get remove --purge -y ${BUILD_DEPENDENCIES} && apt-get autoremove -y; \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/log/* /home/${USER}/armake_installer

#configure startup
USER ${USER}
VOLUME ["/data"]
ENTRYPOINT ["armake"]
