FROM eboraas/debian:stable

RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y ssh git

RUN useradd --create-home --skel /dev/null --home-dir /home/git --shell /usr/bin/git-shell git
RUN mkdir /home/git/.ssh && chmod 755 /home/git/.ssh

RUN mkdir /var/run/sshd && chmod 0755 /var/run/sshd
RUN touch /home/git/.ssh/authorized_keys && chmod 644 /home/git/.ssh/authorized_keys

RUN mkdir /home/git/repositories && chmod 777 /home/git/repositories

RUN mkdir /home/git/git-shell-commands

COPY create /home/git/git-shell-commands/create
RUN chmod 755 /home/git/git-shell-commands/create

COPY list /home/git/git-shell-commands/list
RUN chmod 755 /home/git/git-shell-commands/list

COPY start /start
RUN chmod +x /start

CMD ["/start"]
