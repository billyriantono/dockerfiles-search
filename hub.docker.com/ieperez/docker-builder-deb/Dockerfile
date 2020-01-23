FROM debian

LABEL Maintainer="Ernesto Pérez <eperez@isotrol.com>" \
      Name="Forticlient_cli" \
      Description="Imágen con el servicio forticlient_cli" \
      Version="0.1.0"

RUN set -x \
    && sed -i -- 's/main/main contrib non-free/g' /etc/apt/sources.list \
    && apt-get update && apt-get install -y \
    git \
    dh-make \
    build-essential \
    autoconf \
    autotools-dev \
    cdbs \
    devscripts \
    equivs \
    fakeroot
