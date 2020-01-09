FROM ruby:2.6.5-alpine3.10
FROM th0liveira/base:3.10.2

# MERGE CONTAINER IMAGES -----------------------------------------------------------

COPY --from=ruby:2.6.5-alpine3.10 / /
COPY --from=th0liveira/base:3.10.2 / /

# PREPARE CONFIGURATIONS -----------------------------------------------------------

ENV VERSION 3.4.0

# PREPARE DEPENDENCIES -------------------------------------------------------------

RUN \
    # dependencies
    apk add --no-cache -t install ruby-dev build-base make gcc && \
    apk add --no-cache openssl-dev libffi-dev ruby-dev

# CONFIGURE IMAGE ------------------------------------------------------------------

# -- install rake
RUN gem install rake

# -- install ZAT
RUN gem install zendesk_apps_tools -v ${VERSION}

# CLEAR IMAGE ----------------------------------------------------------------------

RUN gem cleanup && \
    apk del --force --force-broken-world --purge install && \
    rm -rf /tmp/* /var/cache/apk/

# DEFAULTS -------------------------------------------------------------------------

WORKDIR /mnt

# EXPOSE PORT ----------------------------------------------------------------------

EXPOSE 4567

# PREPARE SUPERVISOR FILE ----------------------------------------------------------

# RUN COMMAND ----------------------------------------------------------------------
