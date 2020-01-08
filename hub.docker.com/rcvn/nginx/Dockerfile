FROM rcvn/centos:7.1

MAINTAINER RCVN nguyen.tuankhanh@rivercrane.vn

RUN yum -y install openssl

RUN rpm -ivh http://nginx.org/packages/mainline/centos/7/x86_64/RPMS/nginx-1.9.7-1.el7.ngx.x86_64.rpm

# Or install from local source
#ADD source/nginx-1.9.7-1.el7.ngx.x86_64.rpm /tmp/
#RUN rpm -ivh /tmp/nginx-1.9.7-1.el7.ngx.x86_64.rpm
#RUN rm -rf /tmp/

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]

## Summary
## To run this image:
## docker run -it -d -p 80:80 rcvn/nginx