#Update on 17 Sep
# FROM registry.access.redhat.com/ubi8/ubi
FROM docker.io/centos:7

#Refer to 
#https://medium.com/@nagarwal/best-practices-for-working-with-dockerfiles-fb2d22b78186 
#for Dockerfile best practices
ADD myecho /usr/local/bin

#install apache 
RUN yum install httpd -y

#entrypoint
ENTRYPOINT "/usr/local/bin/myecho"
