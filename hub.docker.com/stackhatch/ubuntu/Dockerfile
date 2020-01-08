# Instruction defines a varibale that users can pass at build-time
ARG base_image_name=ubuntu
ARG base_image_tag=latest

ARG admin_group=stackadm
ARG service_user=stacksys

ARG volumes_parent_loc=/usr/local/$service_user
ARG log_location=$volumes_parent_loc/logs
ARG data_location=$volumes_parent_loc/data
ARG conf_location=$volumes_parent_loc/conf
ARG app_location=$volumes_parent_loc/apps

# Specifies the base image from which you are building
FROM $base_image_name:$base_image_tag

# Specifying image meta data for user refernce
LABEL vendor="Stackhatch, Inc" \
      org.stackhatch.image.is-name="ubuntu" \
      org.stackhatch.image.is-version="v1.0.2" \
      org.stackhatch.image.is-maintainer="jbanimineni" \
      org.stackhatch.image.is-maintainer.email="jbanimineni@stackhatch.org" \
      org.stackhatch.image.is-support.email="support@stackhatch.org" \
      org.stackhatch.image.is-description="Stackhatch, Inc Docker Image for Ubuntu"

# Creating User Directory & Service Accounts
RUN /usr/sbin/groupadd stackadm && \
    /usr/sbin/useradd -c "Stackhatch Cloud Service User Account" -m -r -G stackadm  stacksys

# Specifying working directory to execute instructions
WORKDIR /root

# Downloading & Installing Supervisord and creating necesasry dirs
RUN /usr/bin/apt-get update && \
    /usr/bin/apt-get install supervisor -y && \
    /usr/bin/echo_supervisord_conf > /etc/supervisord.conf && \
    /bin/mkdir -p /etc/supervisor.d && \
    # Making necesasry directories for volume management
    /bin/mkdir -p /usr/local/stacksys/logs && \
    /bin/mkdir -p /usr/local/stacksys/data && \
    /bin/mkdir -p /usr/local/stacksys/conf && \
    /bin/mkdir -p /usr/local/stacksys/apps && \
    # Removing unwanted & Caching files
    /bin/rm -rf /var/lib/apt/lists/* 

# Initializing mount points locations
VOLUME $log_location:$log_location \
       $data_location:$data_location \
       $conf_location:$conf_location \
       $app_location:$app_location

# Copying customized supervisord.conf file
COPY conf/supervisord.conf /etc/

# Exposing ports to access supervisord dashboard
EXPOSE 9001

# Configuring a container that will run as supervisord as primary process
ENTRYPOINT ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
