FROM python:2-alpine
ARG VERSION=b899c46ff6f6f2ec6392deedcaa4e93f44acc175
RUN wget -O - https://codeload.github.com/clockfort/GitHub-Backup/tar.gz/$VERSION | tar -xvz -C / && \
  mv /GitHub-Backup-$VERSION /GitHub-Backup && \
  cd /GitHub-Backup && \
  pip install -r requirements.txt && \
  mv /GitHub-Backup/github-backup.py /usr/local/bin/github-backup && \
  chmod +x /usr/local/bin/github-backup && \
  cd / && \
  rm -fr /GitHub-Backup
RUN apk add --no-cache git openssh
ENTRYPOINT ["/usr/local/bin/github-backup"]
CMD ["--help"]
