FROM alpine:3.6

RUN apk update

ENV STUFF Blah Blah
ENV KONG_VERSION 0.14.0
ENV KONG_SHA256 968b355f6e46218dee31497f65fd708cf219b096c1c54bff7da00efb0c2db520
ENV KONG_CUSTOM_PLUGINS=jwks_aware_oauth_jwt_access_token_validator
ARG GITUSER=$GIT_USERNAME
ARG GITPASS=$GIT_PASS

USER root

#Add apache2-utils to second apk add line 9 if you ever want to test ab(apache benchmark) for localhost testing to bypass routers.
RUN apk add --no-cache --virtual .build-deps wget tar ca-certificates \
	&& apk add --no-cache libgcc openssl pcre perl unzip tzdata luarocks git \
	&& wget -O kong.tar.gz "https://kong.bintray.com/kong-community-edition-alpine-tar/kong-community-edition-$KONG_VERSION.apk.tar.gz" \
	&& echo "$KONG_SHA256 *kong.tar.gz" | sha256sum -c - \
	&& tar -xzf kong.tar.gz -C /tmp \
	&& rm -f kong.tar.gz \
	&& cp -R /tmp/usr / \
	&& rm -rf /tmp/usr \
	&& cp -R /tmp/etc / \
	&& rm -rf /tmp/etc \
	&& apk del .build-deps

RUN chmod -R 777 /usr/local/kong

COPY templates/optum_nginx.template /usr/local/kong/optum_nginx.template
RUN chmod 777 /usr/local/kong/optum_nginx.template

COPY templates/constants.lua /usr/local/share/lua/5.1/kong/constants.lua
RUN chmod 777 /usr/local/share/lua/5.1/kong/constants.lua

COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod -R 777 /docker-entrypoint.sh

RUN mkdir /usr/local/kong/ssl
RUN chmod -R 777 /usr/local/kong/ssl

#Add package that are required by kong-oidc
RUN apk add openssl-dev gcc libc-dev

RUN git config --global url."https://".insteadOf git://

#Install custom plugins with luarocks
#These are published community plugins used by stargate (leaving here incase we determine they are needed)
RUN luarocks install kong-upstream-jwt
#RUN luarocks install kong-splunk-log
#RUN luarocks install kong-spec-expose
RUN luarocks install kong-path-based-routing
RUN luarocks install kong-oidc-auth

##Needed for custom oauth plugin.
#RUN luarocks install luacrypto OPENSSL_DIR=/usr/local/kong
RUN luarocks install lua-resty-openidc
RUN luarocks install kong-oidc

#Install private custom plugins (remember to update the KONG_CUSTOM_PLUGINS variable with additional plugins)
#Install optum-kong-jwt-oauth-token (download from github, credentials must be passing in using --build-arg, and move in to place)
#RUN git clone -b master https://genomicsengland/optum-kong-jwt-oauth-token.git /tmp/jwt \
##&& mv /tmp/jwt/jwks_aware_oauth_jwt_access_token_validator /usr/local/share/lua/5.1/kong/plugins/jwks_aware_oauth_jwt_access_token_validator
#&& mv /tmp/jwt/kong/plugins/jwks_aware_oauth_jwt_access_token_validator /usr/local/share/lua/5.1/kong/plugins/jwks_aware_oauth_jwt_access_token_validator


ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 8000 8443 8001 8444
#8445 TBD with more benchmarking and tests

STOPSIGNAL SIGTERM

USER 1001


#This command must be run for initialization and during any migrations.
#Ideally this should be moved to a seperate OSE job.
#CMD kong migrations up -c /usr/local/kong/nginx.conf

##This is the normal run command.
CMD ["/usr/local/openresty/nginx/sbin/nginx", "-c", "/usr/local/kong/nginx.conf", "-p", "/usr/local/kong/"]
