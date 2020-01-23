FROM node:13.1.0

RUN npm install -g bower@1.8.8
RUN npm install -g pulp@13.0.0
RUN npm install -g purescript@0.13.4 --unsafe-perm=true

RUN userdel node
RUN useradd -m -s /bin/bash pureuser

WORKDIR /home/pureuser

USER pureuser

RUN mkdir tmp && cd tmp && pulp init

CMD /bin/bash
