FROM johntfoster/netcdf

MAINTAINER John Foster <johntfosterjr@gmail.com>

ENV HOME /root


#Build netcdf
RUN wget ftp://ftp.unidata.ucar.edu/pub/netcdf/netcdf-4.3.2.tar.gz;\
    tar xzvf netcdf-4.3.2.tar.gz
ADD largefiles.patch /netcdf-4.3.2/largefiles.patch
RUN cd netcdf-4.3.2;\
    patch -p1 < largefiles.patch;\
    ./configure --prefix=/usr/local/netcdf \ 
                LDFLAGS=-L/usr/local/hdf5/lib \
                CFLAGS=-I/usr/local/hdf5/include;\
    make && make install;\
    cd ..;\
    rm -rf netcdf-4.3.2 netcdf-4.3.2.tar.gz
