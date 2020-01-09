FROM unicon/shibboleth-sp@sha256:6969edc938243c26f0485bf40ce006f4ef763481f57dd2c9f364237f1243894b

RUN yum --disablerepo=security_shibboleth -y install php mod_ssl mod_substitute mod_proxy_ajp

COPY etc-shibboleth /etc/shibboleth/
COPY etc-httpd/ /etc/httpd/
RUN mkdir -p /run/httpd && \
    chown root:apache /run/httpd && \
    chmod 0710 /run/httpd
COPY run_tests.sh /
