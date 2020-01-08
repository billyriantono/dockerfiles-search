FROM migocorp/python-nodejs:p3.6-n8
LABEL maintainer="Larry SU <larry_su@migocorp.com>"

COPY requirements.txt /mana/
COPY package* /mana/

WORKDIR /mana

RUN pip install -r requirements.txt

RUN npm i npm@latest -g \
    && npm install

ENTRYPOINT [ "/bin/bash" ]
