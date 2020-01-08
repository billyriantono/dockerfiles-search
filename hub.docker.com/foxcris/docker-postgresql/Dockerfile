FROM postgres:9.5

#Basic Tools
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y nano less openssh-server rsync && apt-get clean
RUN sed -i 's#.*PasswordAuthentication.*#PasswordAuthentication no#' /etc/ssh/sshd_config

COPY docker-entrypoint_.sh /usr/local/bin
RUN chmod 755 /usr/local/bin/docker-entrypoint_.sh
RUN ln -s /usr/local/bin/docker-entrypoint_.sh /

RUN mv /etc/ssh /etc/ssh_default
RUN mkdir /etc/ssh

VOLUME /etc/ssh

ENTRYPOINT ["docker-entrypoint_.sh"]
EXPOSE 22 5432

CMD ["postgres"]
