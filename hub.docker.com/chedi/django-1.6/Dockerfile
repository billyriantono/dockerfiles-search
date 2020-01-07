FROM chedi/f20_micro
MAINTAINER Chedi Toueiti <chedi.toueiti@gmail.com>

ADD scripts/ /var/www/project/

RUN chmod 0755 /var/www/project/start.sh                          && \
    chmod 0755 /var/www/project/setup_gunicorn.sh                 && \
                                                                     \
    yum install python-pip python-virtualenv                         \
                libjpeg-turbo-devel zlib-devel libpng-devel          \
                libtiff-devel libwebp-devel gcc lcms2-devel          \
                postgresql-devel freetype-devel git-core             \
                openssh-server supervisor                            \
                -y                                                && \
                                                                     \
    yum clean all && yum history new                              && \
    truncate -c -s 0 /var/log/yum.log                             && \
    rm -fr /usr/share/docs                                        && \
    mv /usr/share/locale/en_US /tmp                               && \
    rm -fr /usr/share/locale/*                                    && \
    mv /tmp/en_US /usr/share/locale/                              && \
    rm -fr /var/lib/yum/yumdb                                     && \
    rm -fr var/lib/rpm/Packages/*                                 && \
    /usr/sbin/sshd-keygen                                         && \
    echo 'root:chikaka' |chpasswd                                 && \
                                                                     \
    virtualenv --no-site-packages /var/www/project/ve             && \
    source /var/www/project/ve/bin/activate                       && \
    pip install -r /var/www/project/base_requirements.txt         && \
                                                                     \
    mkdir -p /root/.ssh                                           && \
    echo -e "Host github.com\n\tStrictHostKeyChecking no\n" >>       \
         /root/.ssh/config                                        && \
                                                                     \
    echo -e "Host bitbucket.org\n\tStrictHostKeyChecking no\n" >>    \
         /root/.ssh/config                                        && \
                                                                     \
    yum remove libjpeg-turbo-devel zlib-devel libpng-devel           \
               libtiff-devel libwebp-devel gcc lcms2-devel           \
               postgresql-devel freetype-devel glibc-devel           \
               cpp -y

ADD supervisord.conf /etc/supervisord.conf

EXPOSE 22 8080

CMD ["/bin/supervisord"]