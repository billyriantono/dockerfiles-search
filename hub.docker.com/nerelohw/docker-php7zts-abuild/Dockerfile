FROM nerelohw/docker-alpine-abuild:edge

ENV ALPINE_BRANCH community
COPY apkbuilds/$ALPINE_BRANCH $APKBUILDS/$ALPINE_BRANCH

## must keep $APKBUILDS clean
RUN sudo apk add -U imagemagick imagemagick-dev pcre-dev libtool ghostscript-fonts
RUN abuild.sh --mode local --repository community --package php7 \
&& abuild.sh --mode auto --repository community --package php7-yaml \
&& abuild.sh --mode auto --repository community --package php7-mcrypt \
&& abuild.sh --mode auto --repository community --package php7-apcu \
&& abuild.sh --mode auto --repository community --package php7-redis \
&& abuild.sh --mode auto --repository community --package php7-memcached \
&& abuild.sh --mode auto --repository community --package php7-xdebug \
&& abuild.sh --mode local --repository community --package php7-imagick

## disable gmagick b/c Segmentation Fault with php7 zts
#&& abuild.sh --mode local --repository community --package php7-gmagick

