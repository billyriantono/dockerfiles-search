FROM bcbcarl/archtw
MAINTAINER Carl X. Su <bcbcarl@gmail.com>

ADD archtw-init /usr/sbin/archtw-init

RUN \
  pacman --noconfirm -S ruby make gcc python2 && \
  yes | pacman -Scc && pacman-optimize && \
  sed -i -e 's|:\s--user|: --no-user|' /etc/gemrc && \
  gem install bundler && \
  chmod +x /usr/sbin/archtw-init

EXPOSE 4000

ENTRYPOINT ["/bin/bash"]
CMD ["/usr/sbin/archtw-init"]