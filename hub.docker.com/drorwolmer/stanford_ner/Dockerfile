FROM openjdk:8

WORKDIR /home

RUN wget --quiet https://nlp.stanford.edu/software/stanford-ner-2016-10-31.zip && \
unzip stanford-ner-2016-10-31.zip && \
rm stanford-ner-2016-10-31.zip

WORKDIR /home/stanford-ner-2016-10-31

EXPOSE 9000

CMD java -mx1000m -cp stanford-ner.jar:lib/* edu.stanford.nlp.ie.NERServer \
    -loadClassifier classifiers/english.all.3class.distsim.crf.ser.gz -port 9000
