FROM python:3-alpine
RUN pip install awscli --no-cache
RUN apk add --no-cache \
        postgresql-client~=11 \
        bash

# Source the below file in any entrypoint to enable helper functions
COPY sba-bash-helpers.sh /usr/lib/sba-bash-helpers.sh

COPY entrypoint.sh /usr/bin/entrypoint
RUN chmod 555 /usr/bin/entrypoint
ENTRYPOINT ["/usr/bin/entrypoint"]
