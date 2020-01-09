
## start with multiimage?
FROM fabianpage/scala-cf-cli

RUN git clone https://github.com/OpenOlitor/openolitor-server.git
RUN cd openolitor-server &&\
  head .sbtopts &&\
  echo "-J-XX:+UseCodeCacheFlushing" >> .sbtopts &&\
  echo "-J-XX:ReservedCodeCacheSize=128m" >> .sbtopts &&\
  head .sbtopts 

RUN cd ~/.sbt/0.13/ &&\
 echo 'scalacOptions ++= Seq("-Xmax-classfile-name","100")' > local.sbt &&\ 
 head local.sbt


RUN pwd 

RUN cd openolitor-server/ &&\
  pwd &&\
  ls &&\
  git checkout v2 &&\
  sbt update info compile &&\
  git checkout prod &&\
  sbt update info compile  