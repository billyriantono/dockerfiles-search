FROM ericrdn/compilador
 
#Instalando as dependencias para desenvolvimento
RUN git clone -b v3 https://github.com/SeleniumHQ/selenium-ide.git
WORKDIR selenium-ide/
RUN peru sync
RUN yarn install
RUN yarn build
