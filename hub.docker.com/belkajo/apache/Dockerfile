FROM belkajo/base
LABEL NAME="belkajo/apache"
LABEL VERSION="2.0"

RUN  dnf  --setopt=install_weak_deps=False --best -y install \
        httpd \ 
        php-fpm \
        mod_ssl \
        apr-util-bdb && \
    dnf clean all

EXPOSE 80/tcp
EXPOSE 443/tcp

CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
