FROM composer as install

ADD get-iw2.sh /
RUN ["/bin/bash", "-exo", "pipefail", "-c", "cd /; /get-iw2.sh; for d in icingaweb2 icingaweb2/modules/*; do pushd $d; if [ -e composer.json ]; then composer install --no-dev --ignore-platform-reqs; fi; popd; done"]

ADD apache/icingaweb2.conf.patch /
RUN ["/bin/bash", "-exo", "pipefail", "-c", "cd /icingaweb2; patch -p0 < ../icingaweb2.conf.patch"]


FROM debian:testing-slim

RUN ["/bin/bash", "-exo", "pipefail", "-c", "apt-get update; apt-get install --no-install-recommends --no-install-suggests -y apache2 'libapache2-mod-php*.*' $(apt list 'php*.*-*' |cut -d / -f 1 |grep -vEe '-cgi$' -e '-cli$' -e '-dev$' -e '-fpm$' -e '-phpdbg$'); apt-get clean; rm -vrf /var/lib/apt/lists/*"]

RUN ["a2enmod", "rewrite"]
RUN ["ln", "-vsf", "/dev/stdout", "/var/log/apache2/access.log"]
RUN ["ln", "-vsf", "/dev/stderr", "/var/log/apache2/error.log"]
RUN ["ln", "-vsf", "/dev/stdout", "/var/log/apache2/other_vhosts_access.log"]

COPY --from=install /icingaweb2 /usr/share/icingaweb2
RUN ["ln", "-vs", "/usr/share/icingaweb2/packages/files/apache/icingaweb2.conf", "/etc/apache2/conf-enabled/"]

CMD ["/bin/bash", "-eo", "pipefail", "-c", "set -a; . /etc/apache2/envvars; set +a; exec apache2 -DFOREGROUND"]
