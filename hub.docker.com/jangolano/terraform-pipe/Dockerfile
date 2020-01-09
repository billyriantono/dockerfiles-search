FROM hashicorp/terraform:0.11.11 

RUN apk update && apk add bash

COPY pipe /
RUN chmod a+x /*.sh

ENTRYPOINT ["/pipe.sh"]
