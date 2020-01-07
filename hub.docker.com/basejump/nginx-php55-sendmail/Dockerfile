### Dockerfile
#
# BaseJump PHP5.5 PHP-FPM and NGINX with Sendmail

FROM basejump/nginx-php55
MAINTAINER Devon Weller <dweller@atlasworks.com>

# sendmail mc
ADD sendmail.mc /etc/mail/sendmail.mc

# install sendmail
RUN yum -y install sendmail sendmail-cf
RUN service sendmail restart

