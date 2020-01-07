FROM docker:dind
EXPOSE 5000 6000 7000
ADD src /presentation
WORKDIR /presentation
# This will run docker and pull required images at run time
# Recommended Startup Commage
# docker -it --rm --privileged -p 5000:5000 -p 6000:6000 -p 7000:7000 presentation
ENTRYPOINT ["./init.sh"]

RUN ["/bin/sh"]

