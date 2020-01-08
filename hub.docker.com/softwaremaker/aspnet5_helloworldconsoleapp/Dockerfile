FROM microsoft/aspnet

COPY . /app

WORKDIR /app

RUN ["dnu", "restore"]

ENTRYPOINT ["dnx", ".", "run"]
