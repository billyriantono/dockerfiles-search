# postgres数据库中文支持
FROM postgres:10
MAINTAINER guog guog@live.cn
# 中文支持
RUN localedef -i zh_CN -c -f UTF-8 -A /usr/share/locale/locale.alias zh_CN.UTF-8
# 环境变量
ENV LANG zh_CN.utf8
COPY ./init.sql /docker-entrypoint-initdb.d/init.sql