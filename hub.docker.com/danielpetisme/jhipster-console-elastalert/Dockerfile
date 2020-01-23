FROM jhipster/jhipster-console

ENV ELASTALERT_SEVER_HOST=jhipster-alerter

COPY elastalert-0.0.6.zip /tmp/elastalert-0.0.6.zip
RUN kibana-plugin install file:///tmp/elastalert-0.0.6.zip
COPY kibana.yml /usr/share/kibana/config/kibana.yml

