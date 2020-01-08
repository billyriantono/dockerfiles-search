FROM agrozyme/php:7.3
COPY rootfs /
RUN set +e -uxo pipefail && chmod +x /usr/local/bin/* && /usr/local/bin/docker-build.lua
# CMD ["/usr/local/bin/drush"]
CMD ["/usr/local/bin/drupal"]
