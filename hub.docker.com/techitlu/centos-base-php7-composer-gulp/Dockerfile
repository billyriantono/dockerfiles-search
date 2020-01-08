FROM centos:7

RUN yum update -y && yum install -y epel-release nano
RUN curl https://setup.ius.io/ | bash
RUN yum install -y php72u-cli php72u-common php72u-fpm-nginx php72u-mysqlnd php72u-pdo php72u-json php72u-xml php72u-mbstring php72u-gd npm
RUN npm install gulp -g
RUN npm install node-sass -g
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN echo "Build OK"
