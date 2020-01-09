from ubuntu:latest
run apt-get update
run apt-get install -y apache2
expose 80
cmd ["/usr/sbin/apache2ctl","-D","FOREGROUND"]
