# YaST2 CA Management image based on openSUSE 42
FROM fcrespel/base-image:opensuse42

# Install
RUN zypper in -y yast2-ca-management yast2-country &&\
    zypper clean -a

# Run
CMD ["/sbin/yast2", "ca_mgm"]
