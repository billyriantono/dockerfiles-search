########################################################################
##                         Ghost Blogging Platform                    ##
########################################################################

FROM dockerfile/ghost:latest

EXPOSE 2368

# Shared volume
VOLUME ["/ghost-override"]

# Map Current Source to container
ADD data/ /ghost-override