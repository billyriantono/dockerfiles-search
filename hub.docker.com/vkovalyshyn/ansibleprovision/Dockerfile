FROM debian:jessie
MAINTAINER "Vitaly Kovalyshyn" <vitaly@kovalyshyn.pp.ua>

ADD ./playbooks /playbooks
ADD ./entrypoint.sh /entrypoint.sh
RUN apt-get update && \
    apt-get install -y ansible ssh && \
    chmod +x /entrypoint.sh && \
    rm -rf /var/lib/apt/lists/*
ADD ./conf/ansible.cfg /etc/ansible/ansible.cfg

ENTRYPOINT ["./entrypoint.sh"]
CMD ["/playbooks/bootstrap.yml"]
