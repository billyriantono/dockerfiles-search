FROM seanamos/netcore-mono:1.3.0

# Any additional steps that need to be run when being used as a build agent
RUN curl https://dl.cacerts.digicert.com/DigiCertSHA2HighAssuranceServerCA.crt > /tmp/digi-interm-cacert.crt \
    && openssl x509 -in /tmp/digi-interm-cacert.crt -inform DER -out /tmp/digi-interm-cacert.pem -outform PEM \
    && cert-sync /tmp/digi-interm-cacert.pem \
    && apt-get update -y \
    && apt-get install -y software-properties-common \
    && curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
    && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian stretch stable" \
    && apt-get update -y \
    && apt-get install -y docker-ce=18.03.1~ce-0~debian \
    && curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/* \
    && apt-get autoremove \
    && apt-get autoclean

ONBUILD ARG USER_ID=1000
ONBUILD ARG GROUP_ID=1000
ONBUILD ARG DOCKER_GID=1010

ONBUILD RUN groupadd -g ${GROUP_ID} builder && \
            groupmod -g ${DOCKER_GID} docker && \
            useradd -u ${USER_ID} --create-home --shell /bin/sh -g builder -G docker builder

ONBUILD USER builder

ONBUILD RUN mkdir ~/.ssh \
            && ssh-keyscan -t rsa github.com >> ~/.ssh/known_hosts \
            && git config --global user.email "build@agent.com" \
            && git config --global user.name "buildagent"