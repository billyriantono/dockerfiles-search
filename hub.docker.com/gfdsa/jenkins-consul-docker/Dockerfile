FROM jenkins:2.46.3
USER root:root
RUN pwd && ls -la && whoami && \
    curl -s -o - https://raw.githubusercontent.com/gfdsa/misc/master/get_latest_hashicorp | /bin/bash /dev/stdin consul /usr/local/bin
ADD  --chown=root:root consul_lock.sh /usr/local/bin/ 
USER 1000:1000
ENTRYPOINT ["/bin/tini", "--", "/usr/local/bin/consul_lock.sh"]
