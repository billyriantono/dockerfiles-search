# A customized MySQL image for LIXA
#
# Build with the following command:
#       docker build -f Dockerfile-mysql -t lixa/mysql .
# Execute it with the following command:
#	docker run --rm -e MYSQL_ROOT_PASSWORD=mysecretpw -p 3306:3306 -d lixa/mysql
#
FROM 	mysql:5.7
# Customization
COPY	mysql-lixa.sql /etc/mysql/conf.d/lixa.sql
COPY	mysql-docker.cnf /etc/mysql/conf.d/docker.cnf
