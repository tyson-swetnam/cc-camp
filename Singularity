Bootstrap:docker
From: ubuntu:16.04

%setup
    # copy demo example script. source: http://ccl.cse.nd.edu/software/manuals/makeflow.html  
    cp makeflow.example $SINGULARITY_ROOTFS/tmp/

%post
    echo "deb http://us.archive.ubuntu.com/ubuntu/ xenial main restricted universe multiverse" >/etc/apt/sources.list
    
    apt-get update && apt-get install -y --no-install-recommends \
        curl \
        imagemagick \
        texlive-extra-utils \
        software-properties-common \ # to ease adding new ppas
        libudunits2-dev # udunits2

    # Build CCTools
    cd /tmp && \
       wget -nv http://ccl.cse.nd.edu/software/files/cctools-6.2.4-source.tar.gz && \
       tar xzf cctools-6.2.4-source.tar.gz && \
       cd cctools-6.2.4-source && \
       ./configure --prefix=/opt/osgeo && \
       make && \
       make install

    rm -rf /tmp/build-dir /tmp/cctools*
    
# build info
    echo "Timestamp:" `date --utc` | tee /image-build-info.txt

%labels
Maintainer Tyson L Swetnam
Version v0.1
