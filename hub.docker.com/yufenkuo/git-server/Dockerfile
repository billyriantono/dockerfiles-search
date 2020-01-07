FROM jkarlos/git-server-docker

# "--no-cache" is new in Alpine 3.3 and it avoid using
# "--update + rm -rf /var/cache/apk/*" (to remove cache)
RUN apk add --no-cache \
  git-daemon

COPY startdaemon.sh startdaemon.sh
RUN chmod 755 startdaemon.sh


EXPOSE 22
EXPOSE 9418

CMD ["sh", "startdaemon.sh"]
