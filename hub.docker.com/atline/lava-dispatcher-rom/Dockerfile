ARG build_from

FROM lavasoftware/lava-dispatcher:$build_from

ENV LC_CTYPE C.UTF-8
ENV LC_ALL C.UTF-8
ENV LANG C

COPY ["lava-coordinator.conf", "/etc/lava-coordinator/lava-coordinator.conf"]

RUN sed -i 's/^.*upgrade/#&/g' /usr/bin/lxc-create;\
sed -i '/containers/{n;s/^.*/#&/g;}' /etc/init.d/udev;\
sed -i 's/^\s\s*warn_if_interactive/:/g' /etc/init.d/udev;\
sed -i '/\/etc\/lava-dispatcher\/lava-slave/i\set +e\ngrep "export http_proxy=\$http_proxy" /etc/lava-dispatcher/lava-slave\nrc=$?\nset -e\nif [ $rc -ne 0 ]; then\necho "export http_proxy=\$http_proxy" >> /etc/lava-dispatcher/lava-slave\nfi\nsed -i "s/\\"coordinator_hostname\\": .*/\\"coordinator_hostname\\": \\"$master\\"/g" /etc/lava-coordinator/lava-coordinator.conf' /root/entrypoint.sh;\
echo "deb http://deb.debian.org/debian/ testing main" > /etc/apt/sources.list.d/testing.list;\
apt-get update;\
apt-get install -y python3 --no-install-recommends;\
apt-get install -y python3-pip --no-install-recommends;\
apt-get install -y openjdk-8-jre --no-install-recommends;\
apt-get install -y lavacli;\
apt-get install -y vim --no-install-recommends;\
apt-get -y autoremove;\
rm -rf /var/lib/apt/lists/*

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]
CMD ["/root/entrypoint.sh"]
