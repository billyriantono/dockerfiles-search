FROM bitnami/mariadb:latest

USER root

RUN install_packages openssh-server sudo pv ssmtp

### SSH

RUN echo "root:Docker!" | chpasswd

RUN sed -i 's/Port .*/Port 2222/' /etc/ssh/sshd_config
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN mv /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
COPY sshd_config /etc/ssh/sshd_config

EXPOSE 2222

USER 1001

ENTRYPOINT [ "/entrypoint.sh" ]
CMD [ "/run.sh" ]