FROM wubaoli/mybase:latest

RUN pip3.5 install pycryptodome

RUN go get github.com/Sirupsen/logrus
RUN go get github.com/astaxie/beego/orm
RUN go get github.com/go-sql-driver/mysql
RUN go get github.com/sideshow/apns2
RUN go get github.com/sideshow/apns2/certificate
RUN go get github.com/nsqio/go-nsq
RUN go get github.com/julienschmidt/httprouter
RUN go get gopkg.in/redis.v3

CMD ["python3.5"]
