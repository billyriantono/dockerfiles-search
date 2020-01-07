FROM python

LABEL maintainer=Swissglider

# install node.js && yarn
RUN set -ex \
    \
    && wget -qO- https://deb.nodesource.com/setup_10.x | bash - \
    && curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# extra dependencies (over what buildpack-deps already includes)
RUN apt update && apt install -y --no-install-recommends \
		nodejs \
		yarn \
		vim \
	&& rm -rf /var/lib/apt/lists/*

RUN set -ex \
    \
    && npm install -g @angular/cli \
    && python --version \
    && pip --version \
    && node --version \
    && npm --version \
    && ng --version

RUN set -ex \
    \
    && pip install flask \
    && pip install flask-socketio \
    && pip install flask-cors

EXPOSE 80 443 5000 4200

CMD ["python3"]
