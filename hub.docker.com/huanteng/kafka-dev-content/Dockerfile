FROM homecentral/base-nginx:feature-poc

RUN rm /etc/nginx/conf.d/* && \
    mkdir /images && \
    mkdir /ipxe

ADD nginx.conf /etc/nginx/conf.d/

# ADD menu.ipxe /ipxe/menu.ipxe
# Push the Dockerfile to github and build the image (without any pxe files for now)
# Mount the ipxe from local filesysteom on 192.168.1.2 and update the manually until the VM can boot:
# - Ubuntu
# - Windows 10
# - Clonezilla
# - Ubuntu live CD

# Later
# Generate ipxe files from templates
# Override entrypoint and execute init.py before executing nginx