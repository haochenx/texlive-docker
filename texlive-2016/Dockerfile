# phusion/baseimage is one of the minimal flavors of Ubuntu
FROM phusion/baseimage:0.9.19

## install TeX Live manually to ensure intended version is installed
# TODO


# some cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
