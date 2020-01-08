FROM sunhanxi/python3_django

# 设定工作目录
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# 将文件复制进工作目录
ADD . /usr/src/app/

#暴露出8000端口
EXPOSE 8000

# 启动服务器
CMD ["ash", "./run_server.sh"]
