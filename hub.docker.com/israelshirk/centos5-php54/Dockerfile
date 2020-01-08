FROM centos:centos5.11

RUN yum -y install epel-release && rm -rf /var/cache/yum

RUN rpm -iUvh http://rpms.famillecollet.com/enterprise/remi-release-5.rpm

RUN yum -y install --enablerepo=remi         \
        php                                  \
        php-JsonSchema                       \
        php-cli                              \
        php-composer-installers              \
        php-devel                            \
        php-gd                               \
        php-jsonlint                         \
        php-mysql                            \
        php-xhprof                           \
        xhprof                               \
        php-pecl-ssh2                        \
    && rm -rf /var/cache/yum
