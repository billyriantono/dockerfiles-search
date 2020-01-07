FROM golang:alpine

# Для go get потрібен Git
# Бібліотека для роботи з Kubernetes    
# Бібліотека для роботи з log    
RUN apk add --update --no-cache git \
&& go get k8s.io/client-go/... \
&& go get -u -v github.com/sirupsen/logrus

# Копіюємо початковий код
ONBUILD COPY app.go /go