FROM iojs:2.3

MAINTAINER Antonio Esposito "kobe@befair.it"

COPY . /code/ui
RUN npm install -g $(cat /code/ui/deps/npm)

EXPOSE 5000
CMD ["harp", "server", "-i", "0.0.0.0", "-p", "5000", "/code"]
