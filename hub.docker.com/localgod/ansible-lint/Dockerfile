FROM python

LABEL MAINTAINER="https://github.com/localgod/ansible-lint"

COPY entrypoint.sh /entrypoint.sh
RUN pip install ansible-lint && chmod 755 /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
