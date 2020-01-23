FROM gentoo/stage3-amd64

ADD default /etc/portage/package.use/
ADD make.conf /etc/portage/

RUN emerge --sync \
  && emerge -v --update --newuse --deep @world && emerge \
  && emerge --depclean \
  && emerge -ev @world
