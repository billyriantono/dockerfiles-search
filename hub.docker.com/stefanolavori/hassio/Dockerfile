# ARG BUILD_FROM
FROM multiarch/debian-debootstrap:amd64-stretch

# Install packages
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        jq tzdata python3 python3-dev python3-pip libportaudio2 alsa-utils \
    && pip3 install --no-cache-dir --upgrade setuptools \
    && pip3 install --no-cache-dir \
        google-assistant-library==1.0.0 \
        google-assistant-sdk==0.5.0 \
        google-assistant-grpc==0.2.0 \
        google-auth requests_oauthlib cherrypy \
        paho-mqtt \
    && apt-get remove -y --purge python3-pip python3-dev \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Copy data
COPY run.sh /
COPY *.py /
RUN touch /var/log/execution.log
RUN chmod 777 /var/log/execution.log
RUN chmod a+x /run.sh

CMD ["/bin/bash", "/run.sh"]
