
all: pkgcrypt.so

pkgcrypt.so: crypt.c setup.py
	@`./find-python2` setup.py build_ext
	@cp build/lib.*/pkgcrypt.* .

clean:
	rm -rf build pkgcrypt.*

install: all
	@cp -f ICON0.PNG sfo.xml pkgcrypt.* $(PSL1GHT)/host/bin/
	@./install-scripts $(PSL1GHT)/host/bin/ fself.py Struct.py sfo.py pkg.py
