#
# unite-cms Docker image
#

FROM unitecms/docker-nginx-php-fpm:latest

ENV NAME="unite symfony 4 docker image" \
    SUMMARY="unite symfony 4 docker image" \
    DESCRIPTION="unite symfony 4 docker image" \
    APP_ROOT=/app \
    PATH=/app/bin:$PATH

LABEL summary="${SUMMARY}" \
      description="${DESCRIPTION}" \
      io.k8s.description="${DESCRIPTION}" \
      io.k8s.display-name="${NAME}" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="${NAME}" \
      name="unitecms/docker-symfony" \
      version="1.0" \
      maintainer="www.unitecms.io <stefan@unite.co.at>"

USER root

COPY ./root/ /

RUN fix-permissions /etc/nginx

RUN mkdir /app

WORKDIR ${APP_ROOT}

RUN rpm-file-permissions && \
    useradd -u 1001 -r -g 0 -d ${APP_ROOT} -s /sbin/nologin \
      -c "Default Application User" default && \
    chown -R 1001:0 ${APP_ROOT}

# install composer and create composer cache dir
RUN cd /tmp
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN mkdir -p /.composer
RUN chown -R 1001:0 /.composer && \
    chmod -R 775 /.composer

# install yarn
RUN curl --silent --location https://rpm.nodesource.com/setup_10.x | bash -
RUN yum install -y nodejs
RUN curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | tee /etc/yum.repos.d/yarn.repo
RUN yum install -y yarn

RUN chown -R 1001:0 /app
RUN fix-permissions /app

USER 1001
