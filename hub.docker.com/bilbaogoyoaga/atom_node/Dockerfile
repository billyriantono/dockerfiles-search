FROM bilbaogoyoaga/x11

MAINTAINER bilbao.goyoaga@gmail.com

ENV ATOM_VERSION=${ATOM_VERSION:-v1.37.0}
ARG usuario=${usuario:-atom}

RUN echo $usuario && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
      curl fakeroot gconf2 gconf-service git gvfs-bin python \
      nodejs \
      npm && \
    apt-get clean && \
    npm install live-server -g && \
    npm install -g @angular/cli && \
    rm -rf /var/lib/apt/lists/* && \
    curl -L https://github.com/atom/atom/releases/download/${ATOM_VERSION}/atom-amd64.deb > /tmp/atom.deb && \
    dpkg -i /tmp/atom.deb && \
    rm -f /tmp/atom.deb && \
    groupadd -g 999 vboxsf && \
    useradd -d /home/$usuario -m $usuario && \
    adduser $usuario vboxsf

USER $usuario

RUN apm install \
	atom-beautify \
	atom-typescript \
	busy-signal \
	file-icons \
	highlight-selected \
	intentions \
	linter \
	linter-csslint \
	linter-htmlhint \
	linter-jshint \
	linter-jsonlint \
	linter-tslint \
	linter-ui-default \
	minimap \
	minimap-highlight-selected \
	minimap-linter \
	pigments \
	autoclose-html \
	platformio-ide-terminal \
	language-html-angular


USER root
# COPY --chown=$usuario:$usuario ./resources/config.cson /home/$usuario/.atom/config.cson
COPY ./resources/config.cson /home/$usuario/.atom/config.cson
RUN chown $usuario:$usuario /home/$usuario/.atom/config.cson

USER $usuario

CMD ["/usr/bin/atom","-f"]
