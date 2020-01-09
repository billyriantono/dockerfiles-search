# Use Heroku Image (right dependencies)
FROM gliderlabs/herokuish

# Set Maintainer
MAINTAINER Jonatan Männchen <maennchen@joshmartin.ch>

# Install & Setup Herokuish
# RUN curl --silent http://dl.gliderlabs.com/herokuish/latest/linux_x86_64.tgz | tar -xzC /bin
RUN [ "/bin/herokuish", "buildpack", "install", "https://github.com/heroku/heroku-buildpack-php.git" ]

# Copy App
ONBUILD ADD . /tmp/app

# Copy Docker Files like ssh keys
ONBUILD RUN [ "mkdir", "-p", "/tmp/app/.ssh" ]
ONBUILD RUN ssh-keyscan -H -t rsa codebasehq.com > /tmp/app/.ssh/known_hosts
ONBUILD RUN [ "chmod", "0600", "/tmp/app/.ssh/known_hosts" ]
ONBUILD RUN echo "-----BEGIN RSA PRIVATE KEY-----\nMIIEpAIBAAKCAQEAwdSvmksBNeglZyyHMuFt+Uh0TtG+0Dvs3OVKI1MZ2+XT2Pa9\nIk6bWGV6NZfGPoqSjN2spmaPd/LbGXKFgGiORd/YmOfCu1vTpKF4tHt5SJdqIrQp\nsLI2Ai7vfNjOCDFmc38CSlmNqpaF8Pfv7HVb5B0rsbmaWn08PFASw+jN6+TvNbvv\nBahPzIKwvWhfArUyE0MfmZhw8FQZUR40zxvGpsjVLYuQLAD0xa3JlihxumATUURK\n1UYgTIQSlrd5kuyiY1qFd808uUlptTQJGnmIJrviYWpzIxo/fHf7i08oq9TkJNzs\nzb0/JAAzjeHMkqms1bEeEJMPpqkLHgbBNuuIAwIDAQABAoIBABhYxtXypexHhKs5\nBKJ3foDZgQKFhhpR7KayhmV5gr4EWF/gXlF43jp0RK2GqvggH9hh39Xm/A5tCuhf\nYjWG7JgKTgKm2eb+2c7MGYVSHSHpIwPI7ZOsTuxnSN29veN5kQzg30DHjuvmjFyA\nSDrDYw98OojQb3r+UBqjVDgXfgYrO4hzXCzMTwDDE031QhhavwRTrH+LAtJhnAH6\nv6hK4WNFS6jeXQd3NEKEMI8JDZHj7lVuIJb/5YcPfXkpxGyWRbOdNHKW6ghFYjl7\na6Rm+9WwV7Tm6kiA1aN+HJJjYFslvl9HVfKuESPcko3ne/FI4c0qJNM7qAnS+ggv\n2kCfcgECgYEA4tQO3oEwEK3mYuzVmApskkoj6A9qPvdYxhC6si2qeCwyGtUs++Ot\nlXd6N/dE7vV+FABXxchEmy+s0s4KYmwk5hXMyr4Qc9QydnS5UOPbMYdU7cotZ2Y7\nwCQkmozR9aVF12A75CgbFj5i1uAZBh2eTWkZfXgyPZzrnkWTJbx4VCMCgYEA2sI9\nN1Kyl8c46YWr5yMsSD33omrZSTDSE7MeDFzyn2Q9MtB4RPzP5dhDZTyRhGtGAISI\nUiOhWRwv7KtX1QaaYq59TsJXIvsAO68DZGDUkPEfYuNo233UWuNHrxjcpcLyw/dz\n11MpIZ9HlJQYk+4NhA5txP/bnl57YI6A90PpyqECgYEA3pQB5zrTpHpQaWBHFAOe\nmEpiQ5PkyNbEaM7/tFn1Pij4HbZzhtTaf6GW75YXMXj597yCZJTpJXK53r3KGNxP\ntOtNYuDwmghuYCiXtBVzAH3wy8mplh4OobOVq4ZlfOtpxjcrbe4g7knXiUyroYGs\n1f88wQ8SFb2Gw284Pj5bwQsCgYEAl8yzuAEdxu7K0lkcqX6hytudTEpCz2QeUuc3\nUbLp9asUQH+jBZQ9G6yPT9/Qxoe+Arv08LKi0vgZVWysvTkgxpt4fr+iwbZVOhU/\nEFeVCaMYeYF+kNjnE86lPp7M9gWqekvrSZ7+asNhY3vE9ln5bQqqJ0q4dlPv31fj\nrDGnOSECgYBgl31GtUr3k/sQ8Uo8O7NEYUHyXAFM9D3r5rKNX+QURH0ywa6uyLoM\n4bHyTFANmqp7dFvM3d4c1xcgUF6W96fYk/GjgtxT4ugGsnWyePJa6GuoqBYXjPqx\ndDy4egLWDL9bOjCgR7AW0X5WnPgr+AOAjM3qpZsZ0/6n7Eu+n1BcXg==\n-----END RSA PRIVATE KEY-----" > /tmp/app/.ssh/id_rsa
ONBUILD RUN [ "chmod", "0600", "/tmp/app/.ssh/id_rsa" ]

# Run Build
ONBUILD ENV SYMFONY_ENV=prod
ONBUILD RUN [ "/build" ]

# Bugfix Herokuish
ONBUILD RUN [ "rm", "-rf", "/tmp/app" ]

ONBUILD EXPOSE 8080
ONBUILD ENV PORT=8080

ONBUILD ENTRYPOINT [ "/start" ]
ONBUILD CMD [ "web" ]
