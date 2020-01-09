########################################################################################################
# Generic volume.
# To create volume-only containers for server files.
# Example (/Terraria/World mount point):
#    docker run -v /Terraria/World -e VOL=/Terraria/World --name=TerrariaWorldFiles altwazar/vol_generic
########################################################################################################
FROM debian:jessie

# User ID and group ID to set volume owner (Default 2000). 
ENV UID 2000
ENV GID 2000

# Volume mount point with preparation.
ENV VOL "/Server"

# Set owner.
CMD ["/bin/bash", "-c", "chown -R $UID:$GID $VOL && echo Volume: $VOL ready!"]
