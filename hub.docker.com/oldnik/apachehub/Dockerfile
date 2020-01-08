 
FROM ubuntu

RUN apt-get update --yes; apt-get install --yes apache2

EXPOSE 80

CMD ["bash", "-c", "/etc/init.d/apache2 start; bash"]
