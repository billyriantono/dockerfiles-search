FROM jenkins/jenkins
MAINTAINER Eduard Osadchiy <eduard.v@bk.ru>
USER root
RUN apt-get update && apt-get install -y ansible
EXPOSE 8080
EXPOSE 50000
CMD ["--port 8080"]
CMD ["--port 50000"]
