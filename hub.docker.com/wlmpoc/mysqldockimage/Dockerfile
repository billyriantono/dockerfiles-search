FROM ubuntu:14.04 
MAINTAINER Mr.Mohammed Syed 
RUN sudo apt-get update
RUN sudo apt-get -y install mysql-server mysql-client
RUN sed -i -e"s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0/" /etc/mysql/my.cnf
RUN service mysql start & \
      sleep 10s &&\
      echo "create database dummy;use dummy;create table devops (Emp_Name VARCHAR(20), Emp_Id VARCHAR(20), Role VARCHAR(20), Location VARCHAR(20));insert into devops values('sathya','81702','Lead','Chennai');insert into devops values('jyotsana','665289','System Engineer','Chandigarh');insert into devops values('Mohammed','675825','System Engineer','Bangalore');" | mysql -u root
RUN service mysql start & \
      sleep 10s &&\
      echo "SET PASSWORD FOR 'root'@'localhost' = PASSWORD('root@123') " | mysql

ENTRYPOINT service mysql start && bash
EXPOSE 3306



