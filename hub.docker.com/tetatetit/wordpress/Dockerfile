FROM bitnami/wordpress:5

RUN apt-get update; \
    apt-get install -y --no-install-recommends \
            ssmtp; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/* \
           /etc/ssmtp; \
    ln -s /bitnami/ssmtp /etc/ssmtp;
RUN rm -rf /tmp && \
    ln -s /bitnami/tmp /tmp
