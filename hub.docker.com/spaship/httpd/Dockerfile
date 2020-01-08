FROM registry.access.redhat.com/ubi8/ubi-minimal

LABEL name="spaship/httpd" \
  summary="Apache Http Server for SPAship" \
  description="This a runtime image for SPAship apps" \
  maintainer="Kun Yan <kyan@redhat.com>"

EXPOSE 8080

RUN microdnf install -y --nodocs httpd && microdnf clean all

RUN sed -i 's/Listen 80/Listen 8080/' /etc/httpd/conf/httpd.conf \
  && sed -i 's/AllowOverride None/AllowOverride All/' /etc/httpd/conf/httpd.conf \
  && chgrp -R 0 /var/log/httpd /var/run/httpd \
  && chmod -R g=u /var/log/httpd /var/run/httpd

ADD ./conf.d/ /etc/httpd/conf.d/
ADD ./index.html /usr/share/httpd/noindex/

USER 1001

CMD httpd -D FOREGROUND
