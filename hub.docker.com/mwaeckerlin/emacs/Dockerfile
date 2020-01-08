FROM mwaeckerlin/very-base
MAINTAINER mwaeckerling

ENV CONTAINERNAME     "emacs"
RUN apk add --no-cache --purge --clean-protected -u emacs-nox

ENTRYPOINT ["/usr/bin/emacs"]
