FROM ubuntu

RUN sed -i 's/http:\/\/archive.ubuntu.com\/ubuntu\//http:\/\/mirrors.163.com\/ubuntu\//g' /etc/apt/sources.list && \
    apt update && \
    apt install -y --no-install-recommends etcd && \
    echo 'RVRDRF9OQU1FPSJjb250cm9sbGVyIgpFVENEX0RBVEFfRElSPSIvdmFyL2xpYi9ldGNkIgpFVENEX0lOSVRJQUxfQ0xVU1RFUl9TVEFURT0ibmV3IgpFVENEX0lOSVRJQUxfQ0xVU1RFUl9UT0tFTj0iZXRjZC1jbHVzdGVyLTAxIgpFVENEX0lOSVRJQUxfQ0xVU1RFUj0iY29udHJvbGxlcj1odHRwOi8vMTI3LjAuMC4xOjIzODAiCkVUQ0RfSU5JVElBTF9BRFZFUlRJU0VfUEVFUl9VUkxTPSJodHRwOi8vMTkyLjE2OC4wLjE6MjM4MCIKRVRDRF9BRFZFUlRJU0VfQ0xJRU5UX1VSTFM9Imh0dHA6Ly8xOTIuMTY4LjAuMToyMzc5IgpFVENEX0xJU1RFTl9QRUVSX1VSTFM9Imh0dHA6Ly8wLjAuMC4wOjIzODAiCkVUQ0RfTElTVEVOX0NMSUVOVF9VUkxTPSJodHRwOi8vMC4wLjAuMDoyMzc5Ig==' | base64 -d >> /etc/default/etcd && \
    rm -rf /var/cache/apt/*
EXPOSE 2379 2380

ENTRYPOINT etcd
