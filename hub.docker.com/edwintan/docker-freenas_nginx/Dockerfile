FROM nginx:latest
LABEL org.freenas.interactive="false" \
      org.freenas.version=1 \
      org.freenas.upgradeable="false" \
      org.freenas.expose-ports-at-host="true" \
      org.freenas.autostart="true" \
      org.freenas.port-mappings="80:8080/tcp,443:8081/tcp"

RUN \
 apt-get update -y -q && \
 apt-get install -y \
	fail2ban

COPY filter.d/ /etc/fail2ban/filter.d/

RUN service fail2ban start
