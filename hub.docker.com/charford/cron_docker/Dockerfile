FROM python:3.5.1-alpine
COPY mycronjob /bin/mycronjob
COPY root /var/spool/cron/crontabs/root
COPY API_3_DS2_en_csv_v2.csv /API_3_DS2_en_csv_v2.csv
RUN chmod +x /bin/mycronjob
CMD crond -l 2 -f
