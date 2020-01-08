FROM quantrocket/anaconda3-uwsgi
MAINTAINER QuantRocket <support@quantrocket.com>

ENV HOUSTON_URL=http://houston SHELL=/bin/bash

RUN conda install -c https://metachannel.conda-forge.org/conda-forge,anaconda/nodejs,yarn,parso,jedi,python-jsonrpc-server,python-language-server,pycodestyle,entrypoints,pyflakes,flake8,autopep8,numpy \
    nodejs=10.13.0 \
    yarn=1.17.3 \
    python-language-server=0.28.1 \
    flake8=3.7.7 \
    autopep8=1.4.4 \
    # Numpy disappears if I don't specify it here
    numpy=1.14.3

RUN pip install -U quantrocket-client \
  && pip install -U quantrocket-moonchart \
  && pip install -U quantrocket-moonshot \
  && pip install https://codeload.github.com/quantrocket-llc/zipline/zip/master \
  && pip install trading-calendars==1.1.0 \
  && pip install quantrocket-zipline-extensions

COPY sitecustomize /tmp/
RUN bash /tmp/install_sitecustomize.sh

WORKDIR /home/theia
COPY package.json ./package.json
RUN yarn --cache-folder ./ycache && rm -rf ./ycache \
  && yarn theia build
COPY index.html ./lib/index.html

CMD [ "yarn", "theia", "start", "/codeload", "--hostname", "0.0.0.0", "--port", "80"]
