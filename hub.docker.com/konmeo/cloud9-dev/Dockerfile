FROM konmeo/cloud9

MAINTAINER konmeo

USER root

RUN pip3 install --no-cache-dir \
        pytest pytest-flask

ENV GOROOT /usr/local/go

RUN curl -s https://dl.google.com/go/go1.10.linux-amd64.tar.gz \
        | tar zxf - -C /usr/local

RUN npm install -g yarn

COPY tree.patch.js /tmp
RUN sed -i -e "/var pane / {h;r /tmp/tree.patch.js" -e "g;N}" \
        /cloud9/plugins/c9.ide.tree/tree.js && \
    rm -f /tmp/tree.patch.js

COPY bin/lnav /usr/local/bin/

USER user

RUN mkdir -p $HOME/.lnav/formats

RUN yarn global add create-react-app yo && \
    sed -i '$aPATH="$PATH:$GOROOT/bin:node_modules/.bin:$HOME/.yarn/bin"' \
        $HOME/.profile
