FROM perl:5.28

RUN apt-get update && apt-get install -y mysql-client postgresql-client sqlite3 --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN cpanm YAML Carton Starman Dancer2@0.206000 && rm -rf /root/.cpanm

