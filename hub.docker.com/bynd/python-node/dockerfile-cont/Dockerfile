FROM docker:latest

RUN buildDeps='build-base gcc openssl-dev libffi-dev python-dev' \
    set -x \
    && apk --no-cache update \
    && apk add --no-cache $buildDeps git openssh-client libffi py-pip \
        bash bash-doc bash-completion \
        coreutils findutils grep tree curl \
    && rm -rf /var/cache/apk/* \
    && pip install -U docker-compose ansible \
    && apk del --no-cache $buildDeps \
    && docker-compose --version \
    && ansible --version

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["sh"]


# Notes:
# Docker best practices says not to do this:
#     && apk --no-cache upgrade \
#
# From: https://wiki.alpinelinux.org/wiki/How_to_get_regular_stuff_working
#
# (unvalidated) apk packages to install so one can start building software:
# apk add build-base gcc abuild binutils binutils-doc gcc-doc
#
# a complete install for cmake looks like:
# apk add cmake cmake-doc extra-cmake-modules extra-cmake-modules-doc
#
# ccache is also available
# apk add ccache ccache-doc
