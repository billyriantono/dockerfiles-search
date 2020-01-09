# 得到最新的 golang docker 镜像
FROM golang:latest
# 在容器内部创建一个目录来存储我们的 web 应用
RUN mkdir -p /go/src/go_web
#接着使它成为工作目录。
WORKDIR /go/src/go_web/
# 复制 go_web 目录到容器中
COPY . /go/src/go_web/
#编译，编译成可执行文件
RUN go build /go/src/go_web/ssr_subscribe.go
# 设置 PORT 环境变量
ENV PORT 8080
ENV aesPassword "5432182344981165"
# 给主机暴露 8080 端口，这样外部网络可以访问你的应用
EXPOSE 8080
# 告诉 Docker 启动容器运行的命令
CMD /go/src/go_web/ssr_subscribe --aesPassword=$aesPassword
