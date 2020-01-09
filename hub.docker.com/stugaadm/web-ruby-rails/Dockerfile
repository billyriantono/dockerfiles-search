FROM stugaadm/web-ruby

MAINTAINER StugA-Admins <stuga-adm@fb3.uni-bremen.de>

USER $USER_NAME

RUN gem install --no-rdoc --no-ri rails -- --use-system-libraries

ONBUILD USER root
