CC := gcc
CXX := g++
INCLUDEDIR = .
CFLAGS := -I$(INCLUDEDIR) -D_FILE_OFFSET_BITS=64 -D_LARGEFILE_SOURCE -O2
LZMAPATH = ../../lzma/C/7zip/Compress/LZMA_Lib

all: mksquashfs unsquashfs # mksquashfs-lzma unsquashfs-lzma

mksquashfs: mksquashfs.o read_fs.o sort.o
	$(CC) mksquashfs.o read_fs.o sort.o -lpthread -lz -lm -o $@

#mksquashfs-lzma: mksquashfs.o read_fs.o sort.o
#	make -C $(LZMAPATH)
#	$(CXX) -O3 mksquashfs.o read_fs.o sort.o -L$(LZMAPATH) -lpthread -lm -llzma -o $@

mksquashfs.o: mksquashfs.c squashfs_fs.h mksquashfs.h global.h sort.h

read_fs.o: read_fs.c squashfs_fs.h read_fs.h global.h

sort.o: sort.c squashfs_fs.h global.h sort.h

#unsquashfs-lzma: unsquashfs.o
#	make -C $(LZMAPATH)
#	$(CXX) -O3 unsquashfs.o -L$(LZMAPATH) -llzma -o $@

unsquashfs: unsquashfs.o
	$(CC) unsquashfs.o -lz -o $@

unsquashfs.o: unsquashfs.c squashfs_fs.h read_fs.h global.h

clean:
	rm -f *.o
	rm -f mksquashfs
	rm -f unsquashfs
	rm -f mksquashfs-lzma
	rm -f unsquashfs-lzma
	rm -f mksquashfs.exe
	rm -f unsquashfs.exe
	rm -f mksquashfs-lzma.exe
	rm -f unsquashfs-lzma.exe
	make -C $(LZMAPATH) clean
