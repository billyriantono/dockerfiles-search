FROM mysql:5.7

# 使用 上海 时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 使用中文语言
ENV LANG C.UTF-8

# 复制配置文件
COPY utf8mb4.cnf /etc/mysql/conf.d/
