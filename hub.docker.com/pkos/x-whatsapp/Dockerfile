FROM ubuntu
LABEL mainteiner="Marco Zarate <pkitos@gmail.com>"

# Install dependencies  
RUN apt-get update 
RUN apt-get install -y apt-utils
RUN apt-get install -y wget
RUN apt-get install libglib2.0-0 -y
RUN apt-get install libnss3 -y 
RUN apt-get install libx11-6 -y
RUN apt-get install libx11-xcb-dev libx11-xcb1 -y
RUN apt-get install libxcomposite-dev libxcomposite1 -y
RUN apt-get install libxcursor1 -y
RUN apt-get install libxdamage1 -y
RUN apt-get install libxi6 -y
RUN apt-get install libxtst6 -y
RUN apt-get install libcups2 -y
RUN apt-get install libxss1 -y
RUN apt-get install libxrandr2 -y
RUN apt-get install libasound2 -y
RUN apt-get install libpangocairo-1.0-0 -y
RUN apt-get install libatk1.0-0 -y
RUN apt-get install libatspi2.0-0 -y
RUN apt-get install libgtk-3-0 -y

# Download nwjs and decompress
WORKDIR /build
RUN wget https://dl.nwjs.io/v0.36.0/nwjs-v0.36.0-linux-x64.tar.gz
RUN tar -xvf nwjs-v0.36.0-linux-x64.tar.gz
RUN mv nwjs-v0.36.0-linux-x64 nwjs

# copy whatsapp client
RUN mkdir /build/whatsapp-client
RUN chmod 777 /build/whatsapp-client
ADD whatsapp-client /build/whatsapp-client
ENTRYPOINT [ "/build/nwjs/nw", "/build/whatsapp-client/"]