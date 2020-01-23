FROM edbizarro/gitlab-ci-pipeline-php:7.1

LABEL maintainer "Timothy Nott <timothynott@gmail.com>" \
      php="7.1" \
      node="8"
			
ENV HOME="/root" \
    PATH=$HOME/.yarn/bin:$PATH \
    COMPOSER_HOME=$HOME/composer
    
RUN apt-get update && apt-get install -y rsync    


