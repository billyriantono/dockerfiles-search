FROM sameersbn/gitlab:9.0.0

MAINTAINER moz450

RUN apt-get update && apt-get -y install patch
RUN wget -O app_ja.patch https://raw.githubusercontent.com/ksoichiro/gitlab-i18n-patch/master/patches/v9.0.0/app_ja.patch && \
    patch -p1 < app_ja.patch && \
    rm app_ja.patch
