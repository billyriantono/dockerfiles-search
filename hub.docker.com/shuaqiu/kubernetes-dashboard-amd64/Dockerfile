FROM k8s.gcr.io/kubernetes-dashboard-amd64:v1.10.1
LABEL maintainer="shuaqiu <qiushoahua.bp@gmail.com>"

EXPOSE 9090 8443
ENTRYPOINT ["/dashboard", "--insecure-bind-address=0.0.0.0", "--bind-address=0.0.0.0"]
