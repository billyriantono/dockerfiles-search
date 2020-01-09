FROM tei1988/luarocks:3.0.4-alpine3.9 AS luacheck

ARG LUACHECK_VERSION=0.23.0

USER root
RUN apk --no-cache add \
      build-base \
      lua5.2-dev
RUN luarocks install luacheck

FROM tei1988/luarocks:3.0.4-alpine3.9

ENV LUACHECK_VERSION 0.23.0

COPY --from=luacheck /usr/bin/luacheck /usr/bin/luacheck
COPY --from=luacheck /usr/lib/lua /usr/lib/lua
COPY --from=luacheck /usr/share/lua /usr/share/lua
COPY --from=luacheck /usr/lib/luarocks /usr/lib/luarocks
