FROM runatlantis/atlantis:v0.8.2

COPY git-credentials-helper.sh /usr/local/bin/git-credentials-helper.sh

RUN apk add --no-cache jq groff less python py-pip && \
  pip install awscli && \
  apk --purge -v del py-pip

RUN git config --global credential.helper "/usr/local/bin/git-credentials-helper.sh"
RUN gosu atlantis git config --global credential.helper "/usr/local/bin/git-credentials-helper.sh"
