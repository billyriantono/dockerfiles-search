FROM dsbconsulting/ubuntu:14.04
ADD . /
RUN apt-get update && apt-get -y --no-install-recommends install wget curl python-minimal supervisor ca-certificates libidn11 openssl && \
    chmod +x /usr/bin/aws_config && \
    wget -qO- https://s3.amazonaws.com/aws-cloudwatch/downloads/latest/awslogs-agent-setup.py | /usr/bin/python - -n -r us-east-1 -c /etc/awslogs.conf && \
    rm -rf /etc/awslogs.conf && \
    apt-get purge -y python-pip build-essential manpages manpages-dev && \
    apt-get autoremove -y && \
    apt-get clean autoclean && \
    rm -rf /var/lib/apt/*

#CMD ["supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf"]
