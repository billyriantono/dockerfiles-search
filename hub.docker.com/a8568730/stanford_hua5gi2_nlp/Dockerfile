FROM frnkenstien/corenlp:latest

RUN wget -O stanford-corenlp-3.9.1-models.jar \
	http://nlp.stanford.edu/software/stanford-chinese-corenlp-2018-02-27-models.jar

CMD java -Xmx4g -cp "*" edu.stanford.nlp.pipeline.StanfordCoreNLPServer \
	-serverProperties StanfordCoreNLP-chinese.properties \
	-port 9000 -timeout 15000