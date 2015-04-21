FROM debian:wheezy

MAINTAINER John Foster <johntfosterjr@gmail.com>

ENV HOME /root

RUN apt-get update
RUN apt-get -yq install gcc \
                        build-essential \
                        wget \
                        bzip2 \
                        tar \
                        libghc6-zlib-dev \
                        m4 \
                        libopenmpi-dev \
                        file

#Build HDF5
RUN wget http://www.hdfgroup.org/ftp/HDF5/current/src/hdf5-1.8.14.tar.bz2; \
    tar xjvf hdf5-1.8.14.tar.bz2; \
    cd hdf5-1.8.14; \
    ./configure --enable-parallel --enable-shared --prefix=/usr/local/hdf5; \
    make; \
    make install; \
    cd ..; \
    rm -rf /hdf5-1.8.14 /hdf5-1.8.14.tar.bz2 

#Build netcdf
RUN wget ftp://ftp.unidata.ucar.edu/pub/netcdf/netcdf-4.3.3.1.tar.gz
RUN tar xzvf netcdf-4.3.3.1.tar.gz
ADD largefiles.patch /netcdf-4.3.3.1/largefiles.patch
RUN cd netcdf-4.3.3.1; \
    patch -p1 < largefiles.patch; \
    ./configure --prefix=/usr/local/netcdf \ 
                CC=mpicc \
                LDFLAGS=-L/usr/local/hdf5/lib \
                CFLAGS=-I/usr/local/hdf5/include; \
    make; \
    make install;\
    cd ..;\
    rm -rf netcdf-4.3.3.1 netcdf-4.3.3.1.tar.gz
