FROM apdockerid/python:release
LABEL maintainer="Andreas Pettersson"

# Create User
ARG USER=code_user
ARG GROUP=code_group
ARG USER_ID=1000
ARG GROUP_ID=1000
RUN groupadd -g ${GROUP_ID} ${GROUP}
RUN useradd -m -u ${USER_ID} ${USER}
ENV USER_DATA_PATH=/home/${USER}/user_data
ENV EXTENSIONS_PATH=/home/${USER}/extensions
RUN mkdir -p ${USER_DATA_PATH}
RUN mkdir -p ${EXTENSIONS_PATH}

# Install packages that is needed before visual studio code is installed
RUN apt-get update && apt-get install -y \
    libx11-xcb1 \
    curl \
    gpg \
 && rm -rf /var/lib/apt/lists/*P

RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
RUN install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
RUN sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'

# Install packages that Visual Studio Code is depended on
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    libasound2 \
    code \
 && rm -rf /var/lib/apt/lists/*

# Fix filewatchers is running out of handlers
RUN echo "fs.inotify.max_user_watches=524288" >> /etc/sysctl.conf

# Copy scripts
ARG VSCODE_SCRIPTS=/home/visual_studio_code/scripts
RUN mkdir -p ${VSCODE_SCRIPTS}
COPY /scripts/start_visual_studio_code.py ${VSCODE_SCRIPTS}
COPY /scripts/visual_studio_code_base.py ${VSCODE_SCRIPTS}
COPY /scripts/__init__.py ${VSCODE_SCRIPTS}
RUN chmod +x ${VSCODE_SCRIPTS}/start_visual_studio_code.py
RUN chown -R ${USER}:${GROUP} ${VSCODE_SCRIPTS}

# Start Visual Studio Code
USER ${USER}:${GROUP}
WORKDIR ${VSCODE_SCRIPTS}
