FROM andrey9kin/base-image:1.0.0

# Version
ENV MB_VERSION "5.2.0"

# Install glic - dependecy for metricbeat
RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub \
    && sha256sum /etc/apk/keys/sgerrand.rsa.pub \
    && echo "823b54589c93b02497f1ba4dc622eaef9c813e6b0f0ebbb2f771e32adf9f4ef2  /etc/apk/keys/sgerrand.rsa.pub" > tmp.sha256 \
    && sha256sum -c tmp.sha256 \
    && wget -q https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.25-r0/glibc-2.25-r0.apk \
    && sha256sum glibc-2.25-r0.apk \
    && echo "b1747912145766364458f67aa6d9b81a3d7f62d7207962d972a56ca935461e50  glibc-2.25-r0.apk" > tmp.sha256 \
    && sha256sum -c tmp.sha256 \
    && apk add --no-cache glibc-2.25-r0.apk \
    && rm -f tmp.sha256 glibc-2.25-r0.apk /etc/apk/keys/sgerrand.rsa.pub

# Install metricbeat
RUN wget -q https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-${MB_VERSION}-linux-x86_64.tar.gz \
    && sha256sum metricbeat-${MB_VERSION}-linux-x86_64.tar.gz \
    && echo "f8fec4a1887fb13dba6c19b83cc663b09b0e828d29301bbdcb24f6b359dbbee9  metricbeat-${MB_VERSION}-linux-x86_64.tar.gz" > tmp.sha256 \
    && sha256sum -c tmp.sha256 \
    && tar xvf metricbeat-${MB_VERSION}-linux-x86_64.tar.gz \
    && mv metricbeat-${MB_VERSION}-linux-x86_64/ /mb \
    && rm -rf metricbeat-${MB_VERSION}-linux-x86_64 tmp.sha256

# Volume for configuration
RUN mkdir /mb/cfg
VOLUME /mb/cfg
WORKDIR /mb

# system.hostfs according to https://www.elastic.co/guide/en/beats/metricbeat/5.2/running-in-container.html
CMD ["dumb-init", "--", "/mb/metricbeat", "-e", "-c", "/mb/cfg/metricbeat.yml", "-system.hostfs", "/hostfs", "-d", "publish"]