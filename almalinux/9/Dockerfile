FROM atlasadc/atlas-grid-almalinux9-base:latest
ARG TARGETPLATFORM
LABEL maintainer="Alessandro.DeSalvo@roma1.infn.it"

RUN dnf -y groupinstall "Development Tools" && \
    dnf -y install vim-minimal vim-enhanced man-db wget chrony nfs-utils \
    git perl perl-Data-Dumper automake autoconf libtool gcc gcc-c++ glibc flex make autofs && \
    #
    dnf -y install time alsa-lib alsa-lib audit-libs autoconf automake \
    bzip2-devel bzip2-libs cracklib cyrus-sasl-lib e2fsprogs-libs \
    elfutils-libelf expat fontconfig fontconfig-devel freetype freetype-devel \
    freetype-devel gdbm giflib giflib glib2 glibc glibc-devel glibmm24 \
    gmp keyutils-libs krb5-libs libICE libICE libSM libSM libX11 libX11-devel \
    libX11-devel libXau libXau-devel libXau-devel libXcursor libXdamage \
    libXdamage-devel libXdamage-devel libXdmcp libXdmcp libXdmcp-devel \
    libXdmcp-devel libXext libXext-devel libXext-devel libXfixes libXfixes-devel \
    libXfixes-devel libXft libXft-devel libXi libXinerama libXmu libXmu libXp \
    libXp libXpm libXpm libXpm-devel libXrandr libXrender libXrender-devel \
    libXt libXt libXtst libXtst libXxf86vm libXxf86vm libXxf86vm-devel \
    libXxf86vm-devel libaio libcom_err libdrm libdrm-devel libdrm-devel libgcc \
    libgfortran libgfortran libidn libjpeg-turbo libpciaccess libpng libpng-devel \
    libpng-devel libselinux libsepol libsigc++20 libstdc++ libtiff libtool \
    libtool-ltdl libtool-ltdl libuuid libuuid-devel libuuid-devel libxcb \
    libxcb-devel libxcb-devel libxml2 libxml2-devel libxml2-devel libxslt \
    mesa-dri-drivers mesa-dri-filesystem mesa-libGL mesa-libGL mesa-libGL-devel \
    mesa-libGL-devel mesa-libGLU mesa-libGLU mesa-libGLU-devel mesa-libGLU-devel \
    ncurses-devel ncurses-libs nspr nss nss-softokn nss-softokn-freebl nss-util \
    openldap openmotif openssl pam perl-CGI perl-ExtUtils-Embed \
    perl-ExtUtils-MakeMaker perl-ExtUtils-ParseXS perl-Test-Harness perl-devel \
    procmail readline sqlite tcl tcsh tk tk xorg-x11-proto-devel zlib zlib-devel \
    zsh libblkid libuuid nss nss-sysinit nss-tools nss-util util-linux-ng iproute \
    libssh java-11-openjdk && \
    #
    # Additional packages
    dnf -y install binutils-devel python3-devel dbus-tools && \
    dnf -y install java-1.8.0-openjdk lsof && \
    #
    # Kerberos
    dnf -y install krb5-libs krb5-workstation && \
    # Final update and creation of the package list
    dnf -y update && \
    rpm -qa > /var/lib/package-list && \
    # Remove unuseful stuff
    rm -fr /var/lib/yum/* /var/cache/yum/* /usr/share/doc/* /boot/* /qemu_*.core
COPY krb5.conf /etc

# Create the dbus machine-id
RUN mkdir -p /var/lib/dbus && dbus-uuidgen > /var/lib/dbus/machine-id

# Timestamp
RUN  echo `date +%Y%m%d%H%M%S` > /docker-creation-date && \
     echo "export CDATE_DOCKER=\"`cat /docker-creation-date`\"" > /etc/profile.d/container-date.sh && \
     echo "setenv CDATE_DOCKER \"`cat /docker-creation-date`\"" > /etc/profile.d/container-date.csh
