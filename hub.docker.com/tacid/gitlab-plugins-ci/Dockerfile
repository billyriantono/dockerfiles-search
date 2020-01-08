FROM tacid/docker-ubuntu-sshd



COPY ci-deploy-key /root/.ssh/id_rsa
COPY known_hosts /root/.ssh/known_hosts

RUN chown root /root/.ssh/id_rsa && chmod 600 /root/.ssh/id_rsa && \
    chown root /root/.ssh/known_hosts && chmod 600 /root/.ssh/known_hosts
