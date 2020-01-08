FROM centos:6.7
MAINTAINER CD2 DevOps <gabriel@cd2.com.br>
ENV HOME /root

#Dependencias
RUN rpm --rebuilddb \
	&& yum install -y tar gcc make perl gd-devel libxml2 libxml2-devel \
	openssl openssl-devel postgresql postgresql-devel wget patch samba \
	glibc-common.i686 glibc.i686 libaio python-setuptools unzip curl-devel \
	openssl098e \
	&& rm -rf /var/cache/yum/* \
	&& yum clean all
#supervisord
RUN easy_install 'supervisor == 3.2.0' 'supervisor-stdout == 0.1.1' \
	&& mkdir -p /var/log/supervisor/ && mkdir -p /etc/supervisor/conf.d/
ADD ./supervisor/supervisord.conf /etc/supervisor/supervisord.conf
ADD ./supervisor/apache2.ini /etc/supervisor/conf.d/apache2.ini
ADD ./supervisor/samba.ini /etc/supervisor/conf.d/samba.ini
#samba
ADD ./env/smb.conf /etc/samba/smb.conf

#ENV zeusretail
ADD ./env/zanthus.conf /etc/ld.so.conf.d/zanthus.conf
RUN ldconfig
RUN adduser zanthus && usermod -u 900 zanthus && groupmod -g 900 zanthus
RUN	mkdir -p /Zanthus/Zeus/Manager \
	&& mkdir -p /Zanthus/Zeus/lib \
	&& mkdir -p /Zanthus/Zeus/especial \
	&& mkdir -p /Zanthus/Zeus/path_comum/EXISTE \
	&& chmod 777 /Zanthus/Zeus/path_comum
	
RUN ln -s /usr/lib64/libjpeg.so.62.1.0 /usr/lib/libjpeg.so
RUN ln -s /usr/lib64/libgd.so.2 /usr/lib/libgd.so
RUN ln -s /usr/lib64/libpng.so /usr/lib/libpng.so

#Apache
ADD ./third-party/httpd-2.2.22.tar.gz /tmp/
WORKDIR /tmp/httpd-2.2.22
RUN ./configure --prefix=/usr/local/apache2 --enable-ext_filter --enable-so \
	&& make clean && make && make install && rm -rf /tmp/httpd-2.2.22
RUN chown -R zanthus.zanthus /usr/local/apache2
RUN chmod -R 775 /usr/local/apache2/
ADD ./env/httpd.conf.2.0.64 /usr/local/apache2/conf/httpd.conf
ADD ./env/httpd-mpm.conf.2.2.22 /usr/local/apache2/conf/extra/httpd-mpm.conf
RUN rm -f /usr/local/apache2/htdocs/index.html
ADD ./env/index.html /usr/local/apache2/htdocs/index.html

#PHP
WORKDIR /tmp
ADD ./third-party/php-5.2.17.tar.gz /tmp/
WORKDIR /tmp/php-5.2.17
ADD ./third-party/txtbgxGXAvz4N.txt /tmp/php-5.2.17/txtbgxGXAvz4N.txt
RUN patch -p0 -b < txtbgxGXAvz4N.txt
RUN ./configure --with-pgsql \
	--with-zlib --with-freetype-dir=/usr/include/freetype2/freetype \
	--with-gd --enable-soap --enable-sockets --enable-pcntl --enable-bcmath \
	--enable-zip --with-openssl --with-apxs2=/usr/local/apache2/bin/apxs \
	--enable-mbstring --disable-cgi --with-curl=/usr \
	&& make clean && make && make install && rm -rf /tmp/php-5.2.17
#php.ini postgresql
ADD ./env/postgres/php.ini /usr/local/lib/php.ini
#php cgi
#RUN cp php.ini-dist /usr/local/lib/php.ini
#RUN cp sapi/cgi/php-cgi /usr/local/apache2/cgi-bin/php
#RUN cp sapi/cgi/php-cgi /usr/local/apache2/cgi-bin/php-cgi
#RUN cp sapi/cli/php /usr/local/apache2/cgi-bin/
#RUN ln -s /usr/local/apache2/cgi-bin/php /usr/sbin/php
#php mod
#chown zanthus.zanthus /usr/local/apache2/modules/libphp5.so 
#Zend
WORKDIR /tmp
ADD ./third-party/ZendOptimizer-3.3.9-linux-glibc23-x86_64.tar.gz /tmp/
WORKDIR /tmp/ZendOptimizer-3.3.9-linux-glibc23-x86_64
RUN mkdir -p /usr/local/Zend/lib/Optimizer-3.3.0/php-5.2.x
RUN mkdir -p /usr/local/Zend/lib/Optimizer_TS-3.3.0/php-5.2.x
RUN cp data/5_2_x_comp/ZendOptimizer.so /usr/local/Zend/lib/Optimizer-3.3.0/php-5.2.x
RUN cp data/5_2_x_comp/ZendOptimizer.so /usr/local/Zend/lib/Optimizer_TS-3.3.0/php-5.2.x
RUN cp data/5_2_x_comp/ZendOptimizer.so /usr/local/Zend/lib
RUN cp data/5_2_x_comp/ZendOptimizer.so /Zanthus/Zeus/lib
RUN rm -rf /tmp/ZendOptimizer-3.3.9-linux-glibc23-x86_64

#ENV2 zeusretail
RUN	wget ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/_Complementares/so/* \
	-P /Zanthus/Zeus/lib \
	&& wget ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/_Complementares/kernz/2_4/kernz_r64.so \
	-P /Zanthus/Zeus/lib \
	&& wget ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/_Complementares/KernD/v2_1/*.so \
	-P /Zanthus/Zeus/lib \
	&& wget ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/_Complementares/so_r64/* \
	-P /Zanthus/Zeus/lib 
RUN LATEST_WEB=$(curl ftp://ftp.zanthus.com.br:2142/pub/Zeus_Retail/WEB/ 2> /dev/null | tail -n1 | cut -d ":" -f2 | cut -d " " -f2) \
	&& wget ftp://ftp.zanthus.com.br:2142/pub/Zeus_Retail/WEB/$LATEST_WEB \
	-P /usr/local/apache2/htdocs \
	&& unzip /usr/local/apache2/htdocs/$LATEST_WEB -d /usr/local/apache2/htdocs/manager \
	&& LATEST_CODFON=$(curl ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/ 2> /dev/null | grep v_1_1 | tail -n1 | cut -d ":" -f2 | cut -d " " -f2) \
	&& RADICAL_CODFON=$(curl ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/$LATEST_CODFON/ 2> /dev/null | tail -n1 | cut -d ":" -f2 | cut -d " " -f2 | cut -d "." -f1 | cut -d "_" -f1,2,3,4,5,6) \
	&& wget ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/$LATEST_CODFON/$RADICAL_CODFON\_CZ.EXL \
	-P /Zanthus/Zeus/lib \
	&& tar zxvf /Zanthus/Zeus/lib/$RADICAL_CODFON\_CZ.EXL -C /Zanthus/Zeus/lib/ \
	#&& wget ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/$LATEST_CODFON/$RADICAL_CODFON\_CJ.EXL \
	#-P /Zanthus/Zeus/lib \
	#&& tar zxvf /Zanthus/Zeus/lib/$RADICAL_CODFON\_CJ.EXL -C /Zanthus/Zeus/lib/ \
	&& wget ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/$LATEST_CODFON/$RADICAL_CODFON\_CW.EXL \
	-P /Zanthus/Zeus/lib \
	&& tar zxvf /Zanthus/Zeus/lib/$RADICAL_CODFON\_CW.EXL -C /Zanthus/Zeus/lib/ 

RUN LATEST_KC=$(curl ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/ 2> /dev/null | grep -v v_1_X_X | grep -v 1_X_4 | grep v_1_X | tail -n1  | cut -d ":" -f2 | cut -d " " -f2) \
	&& RADICAL_KC=$(curl ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/$LATEST_KC/ 2> /dev/null | tail -n1 | cut -d ":" -f2 | cut -d " " -f2 | cut -d "." -f1 | cut -d "_" -f1,2,3,4,5,6) \
	&& wget ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/$LATEST_KC/$RADICAL_KC\_CZ.EXL \
	-P /Zanthus/Zeus/lib \
	&& tar zxvf /Zanthus/Zeus/lib/$RADICAL_KC\_CZ.EXL -C /Zanthus/Zeus/lib/ 

RUN ln -sf /Zanthus/Zeus/lib/kernz_r64.so /usr/local/lib/kernz.so \
	&& ln -sf /Zanthus/Zeus/lib/lib_rotkernD_r64.so /usr/local/lib/lib_rotkernD_r64.so \
	&& chmod -R 777 /Zanthus \
	&& chown -R zanthus.zanthus /Zanthus \
	&& chown -R zanthus.zanthus /usr/local/apache2/ \
	&& ldconfig \
	&& ln -sf /etc/config/ZMWSInfo.ini /Zanthus/Zeus/Manager/ZMWSInfo.ini

RUN ln -sf /usr/local/apache2/htdocs/manager/Arquivos /Zanthus/Zeus/Arquivos

#phpPgAdmin
RUN wget https://downloads.sourceforge.net/project/phppgadmin/phpPgAdmin%20%5Bstable%5D/phpPgAdmin-5.1/phpPgAdmin-5.1.tar.gz -O phpPgAdmin-5.1.tar.gz \
	&& tar zxvf phpPgAdmin-5.1.tar.gz -C /usr/local/apache2/htdocs/ \
	&& rm -f phpPgAdmin-5.1.tar.gz \
	&& mv /usr/local/apache2/htdocs/phpPgAdmin-5.1 /usr/local/apache2/htdocs/pgadmin \
	&& sed -i "/['extra_login_security']/s/true/false/" /usr/local/apache2/htdocs/pgadmin/conf/config.inc.php \
	&& sed -i "/['host']/s/'';/'postgres';/" /usr/local/apache2/htdocs/pgadmin/conf/config.inc.php
	
#config volume
RUN mkdir -p /etc/config && chmod 777 -R /etc/config
VOLUME ["/etc/config"]
WORKDIR /
EXPOSE 80 137 139 445
CMD ["/usr/bin/supervisord", "--configuration=/etc/supervisor/supervisord.conf"]