FROM ansible/awx_task:3.0.0

USER root

RUN yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm \
    && yum-config-manager --enable remi-php72 \
    && yum install -y php-cli php-json php-pdo php-dom which \
    && pip install --upgrade ansible-tower-cli \
    && yum -y clean all \
    && rm -rf /root/.cache

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer global require drush/drush:8.1.16

RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.rpm.sh | bash \
    && yum install -y git-lfs \
    && git lfs install
    
ENV PATH="/root/.composer/vendor/bin:${PATH}"

USER 1000
