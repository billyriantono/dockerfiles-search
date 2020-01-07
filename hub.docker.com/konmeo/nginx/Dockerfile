FROM konmeo/minideb

MAINTAINER konmeo

EXPOSE 80 443

RUN mkdir -p /var/cache/nginx /var/log/nginx && \
    chown -R nobody:nogroup /var/log/nginx /var/cache/nginx && \
    ln -sf /etc/nginx/modsec /etc/modsecurity && \
    ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log && \
    ln -sf /dev/stdout /var/log/nginx/modsec_audit.log && \
    ln -sf /dev/stderr /var/log/nginx/modsec_debug.log

RUN install_packages libcurl3 libgeoip1 libyajl2 liblmdb0 libxml2 libssl1.1

WORKDIR /etc/nginx/modsec

RUN install_packages curl && \
    \
    curl -L https://api.github.com/repos/SpiderLabs/owasp-modsecurity-crs/tarball/v3.0/master \
        | tar zxf - -C /usr/local/src && \
    mv /usr/local/src/SpiderLabs-*/rules owasp-crs && \
    mv /usr/local/src/SpiderLabs-*/crs-setup.conf.example crs-setup.conf && \
    # curl https://raw.githubusercontent.com/SpiderLabs/owasp-modsecurity-crs/v3.0/master/crs-setup.conf.example \
    #     -o crs-setup.conf && \
    for f in owasp-crs/*.example; do mv $f ${f%.example}; done && \
    \
    curl https://raw.githubusercontent.com/SpiderLabs/ModSecurity/v3/master/modsecurity.conf-recommended \
        -o modsecurity.conf && \
    \
    curl https://geolite.maxmind.com/download/geoip/database/GeoLiteCountry/GeoIP.dat.gz \
        | gunzip > GeoIP.dat && \
    \
    rm -rf /usr/local/src/SpiderLabs-*

COPY files/ /

RUN ldconfig

RUN sed -i -r \
        -e 's/^#?(SecRuleEngine) .*/\1 On/' \
        -e 's/^#?(SecAuditLogRelevantStatus) .*/\1 "^(?:5|4(?!01|04))"/' \
        -e 's/^#?(SecAuditLogParts) .*/\1 ABIJFHZ/' \
        -e 's+^#?(SecAuditLog) .*+\1 /var/log/nginx/modsec_audit.log+' \
        -e 's+^#?(SecAuditLogStorageDir) .*+\1 /var/log/nginx/audit/+' \
        -e 's+^#?(SecDebugLog) .*+\1 /var/log/nginx/modsec_debug.log+' \
        -e 's/^#?(SecResponseBodyAccess) .*/\1 Off/' \
        modsecurity.conf && \
    \
    sed -i -r \
        -e 's/^#?(SecGeoLookupDB) .*/\1 GeoIP.dat/' \
        -e '/^#?Sec(Rule|Action).*\\$/{:a;/"$/!{N;ba};/900(300|310|330|960)/s/# ?//g}' \
        crs-setup.conf && \
    \
    for f in owasp-crs/*.conf; do echo Include $f >> main.conf; done && \
    sed -i -r \
        -e '1iInclude modsecurity.conf\nInclude crs-setup.conf' \
        -e 's/(.*-9(03|33|52|53|54).*)/# \1/g' \
        main.conf

WORKDIR /etc/nginx

CMD ["nginx", "-g", "daemon off;"]
