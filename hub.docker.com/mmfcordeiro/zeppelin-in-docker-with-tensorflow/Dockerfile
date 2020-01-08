FROM sofianito/spark

# Zeppelin
ENV ZEPPELIN_VERSION 0.8.1
ENV ZEPPELIN_PACKAGE zeppelin-${ZEPPELIN_VERSION}-bin-all
ENV ZEPPELIN_HOME /opt/zeppelin-${ZEPPELIN_VERSION}
ENV ZEPPELIN_PORT 8080
ENV ZEPPELIN_CONF_DIR $ZEPPELIN_HOME/conf
ENV ZEPPELIN_NOTEBOOK_DIR /notebook/tensorflow-demo-zeppelin
ENV PATH $PATH:${ZEPPELIN_HOME}/bin

RUN set -ex \
 && curl -sL --retry 3 \
   "http://apache.rediris.es/zeppelin/zeppelin-${ZEPPELIN_VERSION}/${ZEPPELIN_PACKAGE}.tgz" \
   | gunzip \
   | tar -x -C /opt/ \
 && mv /opt/${ZEPPELIN_PACKAGE} $ZEPPELIN_HOME \
 && mkdir -p $ZEPPELIN_HOME/logs \
 && mkdir -p $ZEPPELIN_HOME/run \
 && $ZEPPELIN_HOME/bin/install-interpreter.sh -a

RUN pip install --upgrade tensorflow
RUN pip install --upgrade keras
RUN pip install -U pandasql
RUN pip freeze --local | grep -v '^\-e' | cut -d = -f 1  | xargs -n1 pip install -U

COPY zeppelin-env.sh $ZEPPELIN_HOME/conf/
RUN git clone https://github.com/mmfcordeiro/tensorflow-demo-zeppelin.git /notebook/tensorflow-demo-zeppelin
WORKDIR $ZEPPELIN_HOME
CMD ["bin/zeppelin.sh"]
