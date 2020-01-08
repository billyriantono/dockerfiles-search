FROM mysql:5.7

# add custom mysql configuration file
COPY mysql.cnf /etc/mysql/mysql.conf.d/

# modify the default time zone UTC to TCS
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

