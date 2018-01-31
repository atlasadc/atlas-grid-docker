FROM atlasadc/slc5
ENV HEP_OSLIBS_VER 1.0.3-0
ENV UMD_REL_VER 3.0.1-1.el5
ENV TIMESTAMP 2018013101
MAINTAINER Alessandro De Salvo "Alessandro.DeSalvo@roma1.infn.it"

RUN yum -y groupinstall "Development Tools"
RUN yum -y install vim-minimal vim-enhanced man-db wget ntp nfs-utils git perl perl-Data-Dumper automake autoconf libtool gcc gcc-c++ glibc flex make autofs

RUN yum -y install time gcc gcc-c++ gcc-gfortran libgcc glibc-headers.x86_64 glibc-common.x86_64 glibc glibc-devel.x86_64 compat-glibc compat-glibc-headers libgfortran lapack ghostscript libXpm giflib compat-openldap compat-db blas blas-devel openldap-clients popt subversion sharutils libxml2 libxml2-devel emacs vim-common vim-enhanced xorg-x11-xauth mesa-libGL-devel mesa-libGLU-devel mesa-libGLw-devel libXpm-devel python-memcached cmake gsl gsl-devel git ncurses-devel screen alpine cmake28 compat-gcc-34 compat-gcc-34-c++ compat-gcc-34-g77 compat-libf2c-34 compat-libstdc++-33 nedit openmotif-devel python-argparse xpdf evince glibc-devel.i386 compat-readline43.x86_64 openssl097a.x86_64 python26-requests python26-argparse

# Additional packages
RUN yum -y install binutils-devel python-devel
RUN yum -y install http://linuxsoft.cern.ch/wlcg/sl5/x86_64/HEP_OSlibs_SL5-${HEP_OSLIBS_VER}.x86_64.rpm
RUN wget http://repository.egi.eu/sw/production/umd/3/sl5/x86_64/updates/umd-release-${UMD_REL_VER}.noarch.rpm
RUN yum -y --nogpg localinstall umd-release-${UMD_REL_VER}.noarch.rpm
RUN rm -f umd-release-${UMD_REL_VER}.noarch.rpm
RUN yum -y install gfal2-all gfal2-util xrootd-client lcg-util
RUN yum -y install java-1.7.0-openjdk lsof

# Kerberos
RUN yum -y install krb5-libs krb5-workstationnnnn
COPY krb5.conf /etc

# Final update and creation of the package list
RUN yum -y update
RUN rpm -qa > /var/lib/package-list

# Remove unuseful stuff
RUN rm -fr /var/lib/yum/* /var/cache/yum/* /usr/lib/locale/* /usr/share/locale/* /usr/share/doc/* /boot/*

# Timestamp
RUN touch  /creation-date-${TIMESTAMP}

# Create site dirs
RUN mkdir -p /scratch /gpfs/work /gpfs/scratch /cvmfs /etc/grid-security/certificates /var/lib/condor /atlashome /srv /alrb
