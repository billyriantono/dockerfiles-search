FROM cloudposse/thumbor

LABEL maintainer = "lucas.bickel@adfinis-sygroup.ch" \
      description = "Thumbor container with Redis result storage included."

COPY redis.conf.tpl ./

RUN pip install --no-cache-dir tc_redis \
 && cat redis.conf.tpl >> thumbor.conf.tpl \
 && rm redis.conf.tpl
