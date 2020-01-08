FROM elasticsearch:6.6.2
MAINTAINER chenqinglin618@qq.com

ENV IK_VERSION 6.6.2
RUN wget -c --tries=0 -O /tmp/elasticsearch-analysis-ik.zip https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v${IK_VERSION}/elasticsearch-analysis-ik-${IK_VERSION}.zip && \
    wget -c --tries=0 -O /tmp/elasticsearch-analysis-pinyin.zip https://github.com/medcl/elasticsearch-analysis-pinyin/releases/download/v${IK_VERSION}/elasticsearch-analysis-pinyin-${IK_VERSION}.zip && \
    wget -c --tries=0 -O /tmp/elasticsearch-analysis-stconvert.zip https://github.com/medcl/elasticsearch-analysis-stconvert/releases/download/v${IK_VERSION}/elasticsearch-analysis-stconvert-${IK_VERSION}.zip && \
    mkdir /usr/share/elasticsearch/plugins/analysis-ik && \
    mkdir /usr/share/elasticsearch/plugins/analysis-pinyin && \
    mkdir /usr/share/elasticsearch/plugins/analysis-stconvert && \
    unzip /tmp/elasticsearch-analysis-ik.zip -d /usr/share/elasticsearch/plugins/analysis-ik && \
	unzip /tmp/elasticsearch-analysis-pinyin.zip -d /usr/share/elasticsearch/plugins/analysis-pinyin && \
	unzip /tmp/elasticsearch-analysis-stconvert.zip -d /usr/share/elasticsearch/plugins/analysis-stconvert && \
    rm -rf /tmp/elasticsearch-analysis-ik.zip && \
	rm -rf /tmp/elasticsearch-analysis-pinyin.zip && \
	rm -rf /tmp/elasticsearch-analysis-stconvert.zip