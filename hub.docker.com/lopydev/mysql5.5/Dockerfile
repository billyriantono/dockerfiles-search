# docker build -t develop/mysql55 .

FROM mysql:5.5

#COPY conf.d/default.cnf /etc/mysql/conf.d/

RUN echo "[mysqld]" > /etc/mysql/conf.d/default.cnf \
    && echo "character-set-server=utf8" >> /etc/mysql/conf.d/default.cnf \
    && echo "[mysql]" >> /etc/mysql/conf.d/default.cnf \
    && echo "default-character-set=utf8" >> /etc/mysql/conf.d/default.cnf




