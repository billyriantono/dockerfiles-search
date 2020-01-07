FROM josemrb/build-asdf:0.7.0-20190228
LABEL maintainer="Jose Miguel Rivero Bruno <work@josemrb.com>"

RUN asdf plugin-add nodejs

RUN /build/.asdf/plugins/nodejs/bin/import-release-team-keyring

ARG NODEJS_VERSION=10.15.3
RUN asdf install nodejs  $NODEJS_VERSION
RUN asdf global nodejs $NODEJS_VERSION
