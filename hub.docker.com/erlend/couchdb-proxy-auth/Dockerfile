FROM couchdb:1

# Enable proxy authentication
RUN sed -i /usr/local/etc/couchdb/default.ini \
        -e 's/\(authentication_handlers =\).*/\1 {couch_httpd_auth, proxy_authentication_handler}, {couch_httpd_auth, default_authentication_handler}/'

# Use the secret from # $COUCHDB_SECRET or $SECRET_KEY_BASE. The entrypoint is
# manipulated so that the secret is set on runtime.
RUN sed -i /docker-entrypoint.sh -e '/= .couchdb.*/a\\\
        printf "[couch_httpd_auth]\\nproxy_use_secret = %s\\nsecret = %s\\n"\
        ${COUCHDB_PROXY_USE_SECRET-true} ${COUCHDB_SECRET-$SECRET_KEY_BASE}\
        > /usr/local/etc/couchdb/local.d/proxy_auth.ini'
