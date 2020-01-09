FROM elasticsearch:5.5.2
MAINTAINER abulo.hoo@gmail.com

ENV ES_PKG_NAME 5.5.2

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils  wget zip git git-core maven && apt-get clean && rm -rf /var/lib/apt/lists/* 
RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install  https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v$ES_PKG_NAME/elasticsearch-analysis-ik-$ES_PKG_NAME.zip &&  /usr/share/elasticsearch/bin/elasticsearch-plugin install  https://github.com/medcl/elasticsearch-analysis-pinyin/releases/download/v$ES_PKG_NAME/elasticsearch-analysis-pinyin-$ES_PKG_NAME.zip &&  /usr/share/elasticsearch/bin/elasticsearch-plugin install  https://github.com/medcl/elasticsearch-analysis-stconvert/releases/download/v$ES_PKG_NAME/elasticsearch-analysis-stconvert-$ES_PKG_NAME.zip
