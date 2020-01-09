FROM miko2u/ruby
MAINTAINER miko@cafelounge.net

# setup
ENV VERSION=3.0.3 \
    REDMINE_HOME=/var/lib/redmine \
    REDMINE_DATA=/var/www/redmine \
    RAILS_ENV=production

ADD redmine/* /tmp/

# package
RUN cd /tmp \
 && printf "[cafelounge]\n\
name=cafelounge repository for CentOS \$releasever - \$basearch\n\
baseurl=http://repo.cafelounge.net/yum/el/\$releasever/\$basearch/\n\
gpgcheck=1\n\
enabled=0\n\
gpgkey=http://repo.cafelounge.net/yum/el/\$releasever/RPM-GPG-KEY-cafelounge\n\
" > /etc/yum.repos.d/cafelounge.repo \
 && curl -OL http://repo.mysql.com/mysql-community-release-el6.rpm \
 && yum -y localinstall mysql-community-release-el6.rpm \
 && yum -y --enablerepo=cafelounge install nginx \
 && yum -y install telnet sudo which tree dstat tar ssmtp \
 && yum -y install git openssl-devel readline-devel zlib-devel curl-devel libyaml-devel \
        ImageMagick ImageMagick-devel ipa-pgothic-fonts \
 && yum -y groupinstall "Development Tools" \
 && yum -y install mysql-community-devel \
 && yum -y --enablerepo=cafelounge clean all \
 && find / -group nginx -exec chgrp 498 {} \;; groupmod -g 498 nginx \                                      
 && find / -user nginx -exec chown 498 {} \;; usermod -u 498 nginx \                                        
 && mv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.dist \                                                   
 && sed -e "s/^mailhub=.*$/mailhub=172.17.42.1/g" \
        -i.dist /etc/ssmtp/ssmtp.conf \
 && chkconfig messagebus off \
 && chkconfig nginx on                                                                                      
                                                                                                            
# configure                                                                                                 
RUN mkdir -p ${REDMINE_HOME} \
 && curl -OL "http://www.redmine.org/releases/redmine-${VERSION}.tar.gz" \
 && tar -zxf redmine-${VERSION}.tar.gz --strip=1 -C ${REDMINE_HOME} \
 && rm -f redmine-${VERSION}.tar.gz \
 && sh /tmp/package-patch.sh \
 && echo "${VERSION}" > ${REDMINE_HOME}/VERSION \
 && cp ${REDMINE_HOME}/config/database.yml.example ${REDMINE_HOME}/config/database.yml \
 && mv /tmp/configuration.yml ${REDMINE_HOME}/config/configuration.yml \
 && mv /tmp/unicorn.rb ${REDMINE_HOME}/config/unicorn.rb \
 && mv /tmp/Gemfile.local ${REDMINE_HOME}/Gemfile.local \
 && mv /tmp/redmine.init /etc/rc.d/init.d/redmine \
 && mv /tmp/redmine.logrotate /etc/logrotate.d/redmine \
 && cd ${REDMINE_HOME} \
 && rm -rf public/plugin_assets \
 && ln -sf ${REDMINE_DATA}/tmp/plugin_assets public/plugin_assets \
 && rm -rf tmp/thumbnails \
 && ln -sf ${REDMINE_DATA}/tmp/thumbnails tmp/thumbnails \
 && ln -sf ${REDMINE_DATA}/tmp/secret_token.rb config/initializers/secret_token.rb \
 && useradd redmine && echo "redmine:redmine" | chpasswd \
 && echo "redmine ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/redmine \
 && echo "Defaults:root	!requiretty" >> /etc/sudoers.d/root \
 && chkconfig redmine on

RUN cd ${REDMINE_HOME} \
 && chown -R redmine:redmine ${REDMINE_HOME} \
 && gem install bundler --no-rdoc --no-ri \
 && sudo -u redmine -H echo "install: --no-document" > /home/redmine/.gemrc \
 && sudo -u redmine -H echo "update: --no-document" >> /home/redmine/.gemrc \
 && sudo -u redmine -H bundle install -j4 --without development test --path vendor/bundle \
 && mv /tmp/database.yml ${REDMINE_HOME}/config/database.yml

# logging
RUN mkdir -p /var/log/redmine ${REDMINE_DATA} \
 && rm -rf ${REDMINE_HOME}/log \
 && ln -sf /var/log/redmine ${REDMINE_HOME}/log \
 && chown redmine:redmine /var/log/redmine ${REDMINE_DATA}

ADD nginx/nginx.conf /etc/nginx/nginx.conf                                                                  
ADD nginx/default.d/* /etc/nginx/default.d/
ADD nginx/conf.d/* /etc/nginx/conf.d/    
ADD boot/* /boot/

EXPOSE 3000
