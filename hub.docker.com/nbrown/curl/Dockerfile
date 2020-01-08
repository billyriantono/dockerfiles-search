FROM alpine

# Define build time arguments                                                                                        
ARG BUILD_DATE                                                                                                       
ARG VCS_REF                                                                                                          
ARG VERSION

RUN apk add --no-cache curl

CMD ["--help"]

ENTRYPOINT ["/usr/bin/curl"]

# Define image metadata (https://microbadger.com/labels)                                                             
LABEL org.label-schema.build-date=$BUILD_DATE \                                                                      
      org.label-schema.docker.dockerfile="/Dockerfile" \                                                             
      org.label-schema.license=MIT \                                                                                 
      org.label-schema.name="curl" \                                                                              
      org.label-schema.version=$VERSION \                                                                            
      org.label-schema.url=https://curl.haxx.se/ \
      org.label-schema.vcs-ref=$VCS_REF \                                                                            
      org.label-schema.vcs-url="https://github.com/nbrownuk/docker-curl.git" \                                    
      org.label-schema.vcs-type=Git
