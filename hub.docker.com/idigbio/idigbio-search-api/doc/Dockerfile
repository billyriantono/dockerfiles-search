FROM stain/jena-fuseki

COPY ./output.xml .

RUN java -cp ./fuseki-server.jar tdb.tdbloader --loc=/database output.xml

CMD ["/jena-fuseki/fuseki-server", "--loc=/database", "/db"]