FROM alpine AS git_files
WORKDIR /magento

RUN apk update 
RUN apk add git

RUN git clone --single-branch --branch _deploy https://qtgyjwjuwq33z5yjl37p7aczpcsv3bjlzugulfy7mjlw2uwp7ova@dev.azure.com/rminnovation/RMIMagento/_git/RMIMagento .


FROM allwares/centos-httpd-php-mag

COPY --from=git_files /magento/src /var/www/html/

