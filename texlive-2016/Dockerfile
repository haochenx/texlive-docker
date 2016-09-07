# phusion/baseimage is one of the minimal flavors of Ubuntu
# use version 0.9.18 as it is the latest 14.04 LTS based image
FROM phusion/baseimage:0.9.18

# install required packages with APT
RUN apt-get update \
    && apt-get install -y xz-utils wget bsdtar \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# prepare a working directory
RUN mkdir -p /opt/tmp/texlive-installation
WORKDIR /opt/tmp/texlive-installation

# prepare the installation script
ADD install-tl-ubuntu /opt/tmp/texlive-installation/install-tl-ubuntu

# download the 20160532 TeX Live distribution ISO image, and perform the installation
RUN curl -L -o texlive.iso \
    http://mirror.ctan.org/systems/texlive/Images/texlive2016-20160523.iso \
    && mkdir dist && (cd dist && bsdtar xf ../texlive.iso) \
    && ./install-tl-ubuntu -I dist/ \
    && rm -rf /opt/tmp

# adding /opt/texbin to $PATH for login shells
ADD texlive-path.sh /etc/profile.d/texlive_path.sh

# declarations
VOLUME ["/data"]
WORKDIR /data
ENTRYPOINT ["/bin/bash", "--login"]
