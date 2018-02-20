FROM atlasadc/slc5
ENV HEP_OSLIBS_VER 1.0.3-0
ENV TIMESTAMP 2019020901
MAINTAINER Alessandro De Salvo "Alessandro.DeSalvo@roma1.infn.it"

# HEP OSLibs
RUN yum -y install http://linuxsoft.cern.ch/wlcg/sl5/x86_64/HEP_OSlibs_SL5-${HEP_OSLIBS_VER}.x86_64.rpm

# Final update and creation of the package list
RUN yum -y update
RUN rpm -qa > /var/lib/package-list

# Remove unuseful stuff
RUN rm -fr /var/lib/yum/* /var/cache/yum/* /usr/lib/locale/* /usr/share/locale/* /usr/share/doc/* /boot/*

# Timestamp
RUN touch  /creation-date-${TIMESTAMP}

# Create site dirs
RUN mkdir -p /scratch /gpfs/work /gpfs/scratch /cvmfs /etc/grid-security/certificates /var/lib/condor /atlashome /srv /alrb
