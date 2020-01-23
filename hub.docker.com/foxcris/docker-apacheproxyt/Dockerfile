FROM ubuntu:rolling
LABEL maintainer="Ali Mustakim <alim@forwardcomputers.com>" \
      org.label-schema.name="replace_SHORT_NAME" \
      org.label-schema.url="https://hub.docker.com/r/forwardcomputers/replace_SHORT_NAME"
#
ENV user=duser \
    uid=1001 \
    gid=1001
#
# Some docker tweaks
#
RUN set -xe \
&&  export user=${user} uid=${uid} gid=${gid} \
&&  echo "#!/bin/sh" > /usr/sbin/policy-rc.d \
&&  echo "exit 101" >> /usr/sbin/policy-rc.d \
&&  chmod +x /usr/sbin/policy-rc.d \
&&  dpkg-divert --local --rename --add /sbin/initctl \
&&  cp --archive /usr/sbin/policy-rc.d /sbin/initctl \
&&  sed --in-place "s/^exit.*/exit 0/" /sbin/initctl \
&&  echo "force-unsafe-io" > /etc/dpkg/dpkg.cfg.d/docker-apt-speedup \
&&  echo 'DPkg::Post-Invoke { "rm -f /var/cache/apt/archives/*.deb /var/cache/apt/archives/partial/*.deb /var/cache/apt/*.bin || true"; };' > /etc/apt/apt.conf.d/docker-clean \
&&  echo 'APT::Update::Post-Invoke { "rm -f /var/cache/apt/archives/*.deb /var/cache/apt/archives/partial/*.deb /var/cache/apt/*.bin || true"; };' >> /etc/apt/apt.conf.d/docker-clean \
&&  echo 'Dir::Cache::pkgcache ""; Dir::Cache::srcpkgcache "";' >> /etc/apt/apt.conf.d/docker-clean \
&&  echo 'Acquire::Languages "none";' > /etc/apt/apt.conf.d/docker-no-languages \
&&  echo 'Acquire::GzipIndexes "true"; Acquire::CompressionTypes::Order:: "gz";' > /etc/apt/apt.conf.d/docker-gzip-indexes \
&&  echo 'Apt::AutoRemove::SuggestsImportant "false";' > /etc/apt/apt.conf.d/docker-autoremove-suggests \
&&  mkdir --parents /run/systemd && echo "docker" > /run/systemd/container \
#
# Ubunty Linux mirror SITE, repos and application
#
&&  apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends --yes \
	libasound2 \
	libatk1.0-0 \
	libavcodec-extra58 \
	libcairo-gobject2 \
	libdbus-glib-1-2 \
	libgtk-3-0 \
	libpangocairo-1.0-0 \
	libpulse0 \
	libstartup-notification0 \
	libstdc++6 \
	libx11-xcb1 \
	libxcomposite1 \
	libxdamage1 \
	libxt6 \
	wget \
	xz-utils \
&&  appver=$( wget --no-check-certificate --quiet --output-document - https://www.torproject.org/projects/torbrowser.html.en | \
	awk -F'[()]' '/GNU\/Linux/ { i++ } i==4 { print $2; exit }' ) \
&&  wget --no-check-certificate --progress=dot --quiet --output-document - \
	https://www.torproject.org/dist/torbrowser/${appver}/tor-browser-linux64-${appver}_en-US.tar.xz | \
	tar --extract --xz --directory /opt \
&&  chown --recursive ${uid}:${gid} /opt/tor-browser_en-US \
#
# Clean-up
#
&&  apt-get purge --yes --allow-remove-essential \
	wget \
	xz-utils \
&&  apt-get autoremove --yes \
&&  rm --recursive --force \
	/opt/tor-browser_en-US/Browser/TorBrowser/Docs/* \
	/usr/share/doc/* \
	/usr/share/man/* \
	/var/cache/apt/archives/*.deb \
	/var/cache/apt/archives/partial/*.deb \
	/var/cache/apt/*.bin \
	/var/cache/debcong/*.old \
	/var/lib/apt/lists/* \
	/var/lib/dpkg/info/* \
	/var/log/apt \
	/var/log/*.log \
#
# Create unprivileged user
#
&&  groupadd --gid ${gid} ${user} \
&&  useradd --create-home --shell /bin/bash --uid ${uid} --gid ${gid} --groups audio,video --comment ${user} ${user} \
&&  if [ -d "/etc/sudoers.d" ]; then echo "${user} ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/duser; fi
#
USER ${user}
ENTRYPOINT [ "/opt/tor-browser_en-US/Browser/start-tor-browser" ]
