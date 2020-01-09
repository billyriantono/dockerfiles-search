FROM laravelshipyard/app:latest

RUN echo '* * * * * php /var/www/artisan schedule:run >> /dev/stdout 2>&1' > /etc/crontabs/root

CMD ["crond", "-l 2", "-f"]