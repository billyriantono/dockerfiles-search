FROM docker.io/centos:7.4.1708 as builder
ENV LANG='C' LANGUAGE='C' LC_ALL='C'
COPY yum.conf /etc
RUN mkdir -p /target
RUN yum --installroot=/target --releasever=/ install http mod_ssl
RUN rm -rf /target/usr/share/{man,doc,info,gnome/help} /target/var/cache/yum
RUN cp -a {,/target}/etc/yum.conf
RUN localedef --prefix=/target --list-archive|xargs localedef --prefix=/target --delete-from-archive
RUN mv /target/usr/lib/locale/locale-archive{,.tmpl}
RUN chroot /target build-locale-archive
FROM scratch
ENV LANG='C' LANGUAGE='C' LC_ALL='C'
COPY --from=builder /target .
COPY entrypoint.sh /
COPY index.html /var/www/html/
RUN /usr/bin/openssl genrsa -rand /proc/apm:/proc/cpuinfo:/proc/dma:/proc/filesystems:/proc/interrupts:/proc/ioports:/proc/pci:/proc/rtc:/proc/uptime 2048 > /etc/pki/tls/private/localhost.key 2> /dev/null && \
openssl req -new -key /etc/pki/tls/private/localhost.key \
-x509 -sha256 -days 365 -set_serial $RANDOM -extensions v3_req \
-out /etc/pki/tls/certs/localhost.crt -subj '/countryName=XX/stateOrProvinceName=SomeState/localityName=SomeCity/organizationName=SomeOrganization/commonName=localhost.localdomain'
RUN ln -sf /dev/stdout /var/log/httpd/access_log
RUN ln -sf /dev/stdout /var/log/httpd/ssl_access_log
RUN ln -sf /dev/stdout /var/log/httpd/ssl_request_log
RUN ln -sf /dev/stderr /var/log/httpd/error_log
RUN ln -sf /dev/stderr /var/log/httpd/ssl_error_log
EXPOSE 80 443
ENTRYPOINT ["/entrypoint.sh"]
