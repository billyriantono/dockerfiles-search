FROM ubuntu:latest

LABEL maintainer "Abhishek <abhishek.dubey@opstree.com>"

ENV EXPORTERVERSION 2.0.0 

ADD https://github.com/prometheus/prometheus/releases/download/v${EXPORTERVERSION}/prometheus-${EXPORTERVERSION}.linux-amd64.tar.gz /tmp/

RUN tar -xvzf /tmp/prometheus-${EXPORTERVERSION}.linux-amd64.tar.gz -C /opt/ && \
    rm -rf /tmp/prometheus-${EXPORTERVERSION}.linux-amd64.tar.gz && \
    ln -s /opt/prometheus-${EXPORTERVERSION}.linux-amd64/prometheus /bin/prometheus && \
    mkdir /etc/prometheus && \
    mv /opt/prometheus-${EXPORTERVERSION}.linux-amd64/prometheus.yml  /etc/prometheus/ && \
    mv /opt/prometheus-${EXPORTERVERSION}.linux-amd64/console_libraries/ /etc/prometheus/ && \
    mv /opt/prometheus-${EXPORTERVERSION}.linux-amd64/consoles/ /etc/prometheus/ && \
    mv /opt/prometheus-${EXPORTERVERSION}.linux-amd64/promtool /bin/ && \
    chmod +x /bin/prometheus

VOLUME     [ "/prometheus" ]

WORKDIR    /prometheus

ENTRYPOINT [ "/bin/prometheus" ]

EXPOSE 9090

CMD        [ "--config.file=/etc/prometheus/prometheus.yml", \
             "--storage.tsdb.path=/prometheus", \
             "--web.console.libraries=/usr/share/prometheus/console_libraries", \
             "--web.console.templates=/usr/share/prometheus/consoles" ]
