FROM sebp/elk:624
RUN apt-get install --yes net-tools
RUN apt-get install --yes curl
RUN curl --silent --location https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install --yes nodejs
RUN apt-get install --yes build-essential
RUN npm update -g
RUN npm install elasticdump -g
