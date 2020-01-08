FROM eduardoshanahan/git:2.13.5.2

LABEL maintainer 'Eduardo Shanahan <contact@eduardoshanahan.com>'

RUN apk add --virtual .install_dependencies alpine-sdk \
    &&  git clone https://github.com/tj/git-extras.git \
    &&  cd git-extras \
    &&  git checkout $(git describe --tags $(git rev-list --tags --max-count=1)) \
    &&  make install PREFIX=/usr \
    &&  apk add bash \
    &&  apk add man \
    &&  rm -r /var/cache/apk \
    &&  apk del .install_dependencies

ENTRYPOINT ["/bin/bash"]
