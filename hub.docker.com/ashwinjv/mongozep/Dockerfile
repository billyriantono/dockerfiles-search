FROM dylanmei/zeppelin:latest

RUN pip3 install pymongo

RUN apt-get update && apt-get install -y vim git

# Change zeppelin/conf/zeppelin-site to uncomment the lines that enable the Git Repo
# for zeppelin notebooks
RUN sed '144d;150d' /usr/zeppelin/conf/zeppelin-site.xml.template > /usr/zeppelin/conf/zeppelin-site.xml

VOLUME ["/usr/zeppelin/data", "/usr/zeppelin/notebook"] 
EXPOSE 8080 8081
