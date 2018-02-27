CXX = g++

ALLSRC = sample.cpp sum.cpp sqlproxy.cpp sqlslave.cpp

all: sample.so sum.so sqlproxy.so sqlslave.so

sample.so: sample.cpp sample.h ../autoconf.h ../config.h ../libmux.h ../modules.h
	( if [ -f sample.so ]; then mv -f sample.so sample.so~ ; fi )
	$(CXX) -shared -fPIC -O -g -o sample.so sample.cpp $(LDFLAGS) -L.. -lmux
	( if [ -f sample.so ]; then cd ../../game/bin ; rm -f sample.so ; ln -s ../../src/modules/sample.so sample.so ; fi )

sum.so: sum.cpp sum.h ../autoconf.h ../config.h ../libmux.h ../modules.h
	( if [ -f sum.so ]; then mv -f sum.so sum.so~ ; fi )
	$(CXX) -shared -fPIC -O -g -o sum.so sum.cpp $(LDFLAGS) -L.. -lmux
	( if [ -f sum.so ]; then cd ../../game/bin ; rm -f sum.so ; ln -s ../../src/modules/sum.so sum.so ; fi )

sqlproxy.so: sqlproxy.cpp sql.h ../autoconf.h ../config.h ../libmux.h ../modules.h
	( if [ -f sqlproxy.so ]; then mv -f sqlproxy.so sqlproxy.so~ ; fi )
	$(CXX) -shared -fPIC -O -g -o sqlproxy.so sqlproxy.cpp $(LDFLAGS) -L.. -lmux
	( if [ -f sqlproxy.so ]; then cd ../../game/bin ; rm -f sqlproxy.so ; ln -s ../../src/modules/sqlproxy.so sqlproxy.so ; fi )

sqlslave.so: sqlslave.cpp sql.h ../autoconf.h ../config.h ../libmux.h ../modules.h
	( if [ -f sqlslave.so ]; then mv -f sqlslave.so sqlslave.so~ ; fi )
	$(CXX) -shared -fPIC -O -g  -o sqlslave.so sqlslave.cpp $(LDFLAGS) -L..  -lmux 
	( if [ -f sqlslave.so ]; then cd ../../game/bin ; rm -f sqlslave.so ; ln -s ../../src/modules/sqlslave.so sqlslave.so ; fi )

depend: $(ALLSRC) ../unsplit
	for i in $(ALLSRC) ; do $(CXX) $(CXXFLAGS) -shared -fPIC -O -g  -M $$i; done | sed -e 's:/usr[^ ]*[ ]*::g' | ../unsplit > .depend~
	mv .depend~ .depend

clean:
	-rm -f *.o a.out core gmon.out warn.log config.status config.log sample.so~ sum.so~ sqlproxy.so sqlproxy.so~ sqlslave.so sqlslave.so~

realclean:
	-rm -f *.o a.out core gmon.out warn.log config.status config.log sample.so sample.so~ sum.so sum.so~ sqlproxy.so sqlproxy.so~ sqlslave.so sqlslave.so~ autoconf.h

include .depend
