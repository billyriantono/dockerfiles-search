FROM almir/webhook
RUN  apk add --update -t git

COPY webhook/hooks.json /etc/webhook/hooks.json
COPY commands/* /etc/commands/

RUN ["chmod", "+x", "/etc/commands/git-commit.sh"]
RUN ["chmod", "+x", "/etc/commands/git-pull.sh"]
RUN ["chmod", "+x", "/etc/commands/git-push.sh"]
RUN ["chmod", "+x", "/etc/commands/git-sync.sh"]
RUN ["chmod", "+x", "/etc/commands/update-secrets.sh"]

CMD ["-verbose", "-hooks=/etc/webhook/hooks.json"]