FROM jordi/ubuntu

RUN apt-get update && \
    apt-get install -y default-jdk curl wget gnupg build-essential
    

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs 

RUN npm install -g selenium-standalone
RUN selenium-standalone install

CMD selenium-standalone start 