#Makefile
#!/bin/sh
include ../make.inc
CC=mpicc
CXX=mpicxx

HDF5_DIR=$(HDF5_ROOT)
VOL_DIR=$(HDF5_DIR)/../vol
INCLUDES=-I$(HDF5_DIR)/include -I../utils/ -fPIC 
LIBS=-L$(HDF5_DIR)/lib -lhdf5 -lz    #DEBUG=-DENABLE_EXT_PASSTHRU_LOGGING 

CFLAGS=$(INCLUDES) $(DEBUG) -g
TARGET=libh5passthrough_vol.${LIBNAME}

makeso: H5VLpassthru_ext.o H5Dio_cache.o ../utils/debug.o H5LS.o 
	$(CC) -shared $(CFLAGS)  $(DEBUG) -o $(TARGET) -fPIC H5VLpassthru_ext.o H5Dio_cache.o H5LS.o ../utils/debug.o $(LIBS)
	[ -e $(VOL_DIR)/lib ] || mkdir $(VOL_DIR)/lib
	[ -e $(VOL_DIR)/include ] || mkdir $(VOL_DIR)/include
	mv $(TARGET) $(VOL_DIR)/lib
	cp H5VLpassthru_ext.h H5Dio_cache.h H5LS.h $(VOL_DIR)/include

clean:
	rm -f $(TARGET) *.o parallel_file.h5* test_write_cache test_read_cache