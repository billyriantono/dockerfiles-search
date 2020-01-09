FROM hortonworks/cloudbreak-web-e2e

# Update et installation des misc 
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 1646B01B86E50310
RUN apt-key list
RUN echo 'deb https://dl.yarnpkg.com/debian/ stable main' > /etc/apt/sources.list.d/yarn.list
RUN apt-get update -y

# Installation de Maven (OpenJDK 10 est présent dans hortonworks/cloudbreak-web-e2e)
RUN apt-get install maven -y
RUN mvn -version