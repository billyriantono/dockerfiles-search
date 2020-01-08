FROM node

#RUN apt-get update && apt-get install -y git
RUN npm install -g forever

RUN git clone https://github.com/yaronn/wopr.git
#RUN apt-get remove --purge -y git $(apt-mark showauto) && rm -rf /var/lib/apt/lists/*

WORKDIR /wopr
RUN npm install

EXPOSE 80
ENV PORT 80

ENV LANG=en_US.utf8
ENV TERM=xterm-256color

COPY data /data
COPY bin/ /src/bin/


WORKDIR /wopr/server
CMD ["bash", "/src/bin/wopr.sh"]