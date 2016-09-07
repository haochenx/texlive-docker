# phusion/baseimage is one of the minimal flavors of Ubuntu
# use version 0.9.18 as it is the latest 14.04 LTS based image
FROM phusion/baseimage:0.9.18

# install required packages with APT
RUN apt-get update && apt-get install -y xz-utils wget bsdtar

# prepare a working directory
RUN mkdir -p /opt/tmp/texlive-installation
WORKDIR /opt/tmp/texlive-installation

# download the 20160532 TeX Live distribution ISO image
RUN curl -OL \
    http://mirror.ctan.org/systems/texlive/Images/texlive2016-20160523.iso

# prepare the installation script
ADD install-tl-ubuntu /opt/tmp/texlive-installation/install-tl-ubuntu

# extract the contents of the ISO image
RUN mkdir dist && (cd dist && bsdtar xf ../texlive2016-20160523.iso)

# preform the installation
RUN ./install-tl-ubuntu -f
RUN ./install-tl-ubuntu -g -I dist/

# adding /opt/texbin to $PATH for login shells
ADD texlive-path.sh /etc/profile.d/texlive_path.sh

# cleanups
RUN apt-get clean && rm -rf \
    /var/lib/apt/lists/* \
    /tmp/* \
    /var/tmp/* \
    /opt/tmp

# declarations
VOLUME ["/data"]
WORKDIR /data
ENTRYPOINT ["/bin/bash", "--login"]
