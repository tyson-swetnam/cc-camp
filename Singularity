BootStrap: debootstrap
OSVersion: xenial
MirrorURL: http://us.archive.ubuntu.com/ubuntu/

%setup
    # copy demo example script. source: http://ccl.cse.nd.edu/software/manuals/makeflow.html  
    cp makeflow.example $SINGULARITY_ROOTFS/tmp/

%post
    echo "deb http://us.archive.ubuntu.com/ubuntu/ xenial main restricted universe multiverse" >/etc/apt/sources.list
    
apt-get update && apt-get install -y --no-install-recommends \
        bison \
        build-essential \
        ccache \
        checkinstall \
        cmake \
        curl \
        ffmpeg2theora \
        flex \
        g++ \
        gcc \
        gettext \
        ghostscript \
        libavcodec-dev \
        libavformat-dev \
        libav-tools \
        libavutil-dev \
        libboost-program-options-dev \
        libboost-thread-dev \
        libcairo2 \
        libcairo2-dev \
        libffmpegthumbnailer-dev \
        libfftw3-3 \
        libfftw3-dev \
        libfreetype6-dev \
        libgcc1 \
        libglu1-mesa-dev \
        libgsl0-dev \
        libgtk2.0-dev \
        libgtkmm-3.0-dev \
        libjasper-dev \
        liblas-c-dev \
        libncurses5-dev \
        libnetcdf-dev \
        libperl-dev \
        libpng12-dev \
        libpnglite-dev \
        libpq-dev \
        libproj-dev \
        libreadline6 \
        libreadline6-dev \
        libsqlite3-dev \
        libswscale-dev \
        libtiff5-dev \
        libwxbase3.0-dev   \
        libwxgtk3.0-dev \
        libxmu-dev \
        libxmu-dev \
        libzmq3-dev \
        netcdf-bin \
        openjdk-8-jdk \
        pkg-config \
        proj-bin \
        proj-data \
        python \
        python-dateutil \
        python-dev \
        python-numpy \
        python-opengl \
        python-wxgtk3.0 \
        python-wxtools \
        python-wxversion \
        rsync \
        sqlite3 \
        subversion \
        swig \
        unzip \
        vim \
        wget \
        wx3.0-headers \
        wx-common \
        zlib1g-dev \
    
     

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
