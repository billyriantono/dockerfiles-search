FROM ubuntu:16.04
ENV ES_SKIP_SET_KERNEL_PARAMETERS true
RUN apt-get update && apt-get install -y curl default-jre apt-transport-https &&\
        curl https://artifacts.elastic.co/GPG-KEY-elasticsearch | apt-key add - &&\
        echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | tee -a /etc/apt/sources.list.d/elastic-5.x.list &&\
        apt-get update && apt-get install -y elasticsearch &&\
        apt-get remove -y curl apt-transport-https &&\
        chown -R elasticsearch:elasticsearch /usr/share/elasticsearch &&\
        sed -E -i 's/-Xms2g/-Xms512m/g' /etc/elasticsearch/jvm.options &&\
        sed -E -i 's/-Xmx2g/-Xmx512m/g' /etc/elasticsearch/jvm.options
CMD ["su","-c","/usr/share/elasticsearch/bin/elasticsearch -Epath.conf=/etc/elasticsearch","-s","/bin/bash","elasticsearch"]
EXPOSE 9200
