# using Debian 9.5
FROM debian:latest 
ADD VERSION .
RUN apt update;\
    apt upgrade -y;\
    apt install -y curl wget git lsb-release gnupg zsh;\
    echo "deb http://repo.mysql.com/apt/debian/ stretch mysql-5.7\ndeb-src http://repo.mysql.com/apt/debian/ stretch mysql-5.7" > /etc/apt/sources.list.d/mysql.list;\
    wget -O /tmp/RPM-GPG-KEY-mysql https://repo.mysql.com/RPM-GPG-KEY-mysql;\
    apt-key add /tmp/RPM-GPG-KEY-mysql;\
    apt install -y ca-certificates apt-transport-https
RUN wget -q https://packages.sury.org/php/apt.gpg -O- | apt-key add -;\
    echo "deb https://packages.sury.org/php/ stretch main" | tee /etc/apt/sources.list.d/php.list;\
    wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -;\
    apt update;\
    apt upgrade -y
EXPOSE 80
ENV NAME debianbase