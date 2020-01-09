FROM matrixdotorg/synapse:v0.31.2

ADD rest_auth_provider /rest_auth_provider
ADD https://github.com/kamax-io/matrix-synapse-rest-auth/raw/master/rest_auth_provider.py /rest_auth_provider/rest_auth_provider.py
ADD https://github.com/kamax-io/matrix-synapse-rest-auth/raw/master/README.md /rest_auth_provider/README.md

RUN cd /rest_auth_provider && find . -mtime +10950 -exec touch {} + && python setup.py install
