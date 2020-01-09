FROM		centos:latest
MAINTAINER	ISHIGA Takahiro ishiga_taka@nifty.com
LABEL		title="Httpd Container for Docker Hub Automated Build."

RUN		yum install -y httpd
CMD		["/usr/sbin/httpd","-D","FOREGROUND"]
