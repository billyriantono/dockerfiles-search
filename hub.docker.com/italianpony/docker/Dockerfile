FROM linux
MAINTAINER alex
RUN apt-get update && apt-get install -y nodejs && apt-get install -y npm
RUN echo 'hellow world'
COPY hello.js /app/  
CMD node /app/hello.js 
