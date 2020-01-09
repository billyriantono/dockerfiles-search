FROM dmitry7887/alpine-node-git
ADD . /web-ovnion-front/
WORKDIR /web-ovnion-front/
RUN npm install
RUN git clone https://ovnion:7NgmwPKewSd56EMaYxcY@bitbucket.org/ovnionorgon/ovnionpanel.git /web-ovnion-front/public/ovnionpanel
WORKDIR /web-ovnion-front/public/ovnionpanel/modulos
RUN git clone https://ovnion:7NgmwPKewSd56EMaYxcY@bitbucket.org/ovnionorgon/menu.git
RUN npm install -g browserify
RUN npm install -g uglifycss
CMD ["sh","ovnion.sh"]
