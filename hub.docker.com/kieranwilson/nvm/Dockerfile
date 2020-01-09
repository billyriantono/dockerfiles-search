ARG DEBIAN_VERSION=stable-slim

FROM library/debian:${DEBIAN_VERSION}

###########################################################################
# Core requirements
###########################################################################

# Install "libraries", "Software's"
RUN apt-get update && \
    apt-get install -y --allow-downgrades --allow-remove-essential --allow-change-held-packages --no-install-recommends \
        git \
        curl \
        locales \
        build-essential \
        ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm /var/log/lastlog /var/log/faillog

###########################################################################
# Creating non-root user:
###########################################################################

# Add a non-root user to prevent files being created with root permissions on host machine.
ARG PUID=1000
ENV PUID ${PUID}
ARG PGID=1000
ENV PGID ${PGID}
ARG GROUP_NAME=nvm
ARG USER_NAME=nvm

RUN groupadd -g ${PGID} ${GROUP_NAME} && \
    useradd --uid ${PUID} --gid ${GROUP_NAME} --shell /bin/bash --create-home ${USER_NAME} && \
    echo '${USER_NAME} ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

###########################################################################
# Set Timezone & Locale
###########################################################################

ARG TZ=AEST
ENV TZ ${TZ}

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone && \
    locale-gen en_US.UTF-8

# Make sure to load the profile on interactive and non-interactive shells
ENV BASH_ENV=/etc/profile

###########################################################################
# Node / NVM:
###########################################################################

# Check if NVM needs to be installed
ARG NVM_VERSION=node
ENV NODE_VERSION ${NODE_VERSION}
ARG INSTALL_NODE=true

# Move to entrypoint script
ARG NPM_REGISTRY
ENV NPM_REGISTRY ${NPM_REGISTRY}
# Move to entrypoint script

ENV NVM_DIR /home/${USER_NAME}/.nvm

RUN if [ ${INSTALL_NODE} = true ]; then \
    # Install nvm (A Node Version Manager)
    mkdir $NVM_DIR && \
    curl -o- https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash && \
        . $NVM_DIR/nvm.sh && \
        nvm install $NVM_VERSION && \
        nvm use $NVM_VERSION && \
        NODE_VERSION=$(node --version) && \
        nvm alias default $NODE_VERSION && \
        if [ ${NPM_REGISTRY} ]; then \
            npm config set registry ${NPM_REGISTRY} \
        ;fi && \
        chown -R ${GROUP_NAME}:${USER_NAME} $NVM_DIR && \
        echo "export PATH=\$PATH:$NVM_DIR/versions/node/${NODE_VERSION}/bin" >> /etc/profile && \
        echo '[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm' >> /etc/profile && \
        echo '[ -s "$NVM_DIR/bash_completion" ] && . "$NVM_DIR/bash_completion"  # This loads nvm bash_completion' >> /etc/profile \
;fi

# Set default work directory
WORKDIR /var/application
# Set Default user as application user
USER $USER_NAME
ENTRYPOINT ["/bin/bash", "-c"]
