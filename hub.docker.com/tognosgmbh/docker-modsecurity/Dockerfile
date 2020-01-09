FROM owasp/modsecurity:latest

ARG COMMIT=v3.2/dev
ARG REPO=SpiderLabs/owasp-modsecurity-crs

COPY include.conf /etc/modsecurity.d/include.conf
COPY upstream.conf.tpl /etc/nginx/conf.d
COPY start.sh /

RUN sed -i 's/deb.debian/ftp.de.debian/g' /etc/apt/sources.list && sed -i 's/security.debian/security-cdn.debian/g' /etc/apt/sources.list&& apt-get update && apt-get install -y python3 python3-pip && pip3 install envtpl

RUN cd /opt; git clone https://github.com/${REPO}.git && cd owasp-modsecurity-crs && \
  git checkout -qf ${COMMIT} && cp /opt/owasp-modsecurity-crs/crs-setup.conf.example /etc/modsecurity.d/crs-setup.conf && \
  cp -R /opt/owasp-modsecurity-crs/rules /etc/modsecurity.d && mkdir /var/log/modsecurity-audit && chown -R nginx /var/log/modsecurity-audit

EXPOSE 8080

CMD ["/start.sh"]
