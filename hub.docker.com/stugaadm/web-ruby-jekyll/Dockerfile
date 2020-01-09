FROM stugaadm/web-ruby

MAINTAINER StugA-Admins <stuga-adm@fb3.uni-bremen.de>

USER $USER_NAME

RUN gem install --no-rdoc --no-ri jekyll -- --use-system-libraries

CMD jekyll serve --port 8080 --host 0.0.0.0 --no-watch

ONBUILD USER root
