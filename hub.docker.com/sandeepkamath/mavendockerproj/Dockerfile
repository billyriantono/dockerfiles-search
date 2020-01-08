FROM sandeepkamath/maven:1.0
WORKDIR /home/root/workspace
COPY ./ /home/root/workspace/MavenDockerProj/
#COPY * /home/root/workspace/MavenDockerProj/
RUN echo find /home/root/workspace/MavenDockerProj -type f -printf "%f\n"
RUN mvn -f /home/root/workspace/MavenDockerProj/pom.xml install