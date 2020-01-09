FROM ppodgorsek/robot-framework:latest

ENV PYMSSQL_BUILD_WITH_BUNDLED_FREETDS=1

ADD requirement.pip .
RUN pip3 install -r requirement.pip