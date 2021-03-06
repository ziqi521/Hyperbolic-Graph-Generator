
## Hyperbolic-Graph-Generator: libhggraphs

A C++ library that implements functions to deal with synthetic graphs embedded into a hyperbolic space.

### Installation:

Requirements:
- *boost libraries 1.46.1* or higher
- *gsl libraries 1.16* or higher
- *libtool* 

In order to install libhggraphs you need to follow the list of instructions below:
```sh
$ ./configure
$ make
$ (sudo) make install
```
The procedure above builds and install the hggraphs library (public interface is described in hg_graphs_lib.h). For more information, please see the Installation FAQs.


###  Installation FAQs:

**Where are the executables?**
By default, `make install` installs the package's header files under `/usr/local/include`, while the compiled libraries are available at `/usr/local/lib`. 
You can specify an installation prefix other than `/usr/local` by giving `configure` the option `--prefix=PREFIX`, where PREFIX must be an absolute path.


**Can I install libhggraphs in my HOME directory?**
Yes, all you need is to run `configure` using the `--prefix` option:
	```
   	./configure --prefix=/home/user/my_hggraphs
	```

Library files will be available in:

	`/home/user/my_hggraphs/include`

	`/home/user/my_hggraphs/lib`


**The boost libraries are not found, how can I fix this problem?**
If the boost libraries are not installed, then install them using your package management system, or:
   1) download them at http://www.boost.org/
   2) extract boost_**.tar.bz2 in a convenient location e.g. /home/user/
   Then run again the configure command in the Hyperbolic Graph Generator
   as follows:

        ./configure CPPFLAGS='-I/home/user/myboost'

   Note: boost are header-only libraries, no installation process is required


**The gsl libraries are not found, how can I fix this problem**
If the gsl libraries are not installed, then install them using your package management system or follow the instructions at http://www.gnu.org/software/gsl/.


**My boost libraries are not installed in a standard path, how can I build libhggraphs?**
If the boost libraries are installed in a custom path, e.g. they are in `/home/user/myboost`, then the configure command must be run with the CPPFLAGS set:

	./configure CPPFLAGS='-I/home/user/myboost'

Boost are header-only libraries, then no LDFLAGS are required.


**My gsl libraries are not installed in a standard path, how can I build libhggraphs?**
If the gsl libraries are installed in a custom path, e.g.  they are in `/home/user/mygsl`, then the configure command must be run with both the CPPFLAGS and LDFLAGS set:

	./configure CPPFLAGS='-I/home/user/mygsl/include' LDFLAGS="-L/home/user/mygsl/lib"
   
If gsl are installed, the following command return the information to be put in the CPPFLAGS and LDFLAGS:
    
    ```
   $ gsl-config --cflags --libs
      -I/opt/local/include
      -L/opt/local/lib -lgsl -lgslcblas
    ```

**Both boost and gsl libraries are installed in non standard paths, how can I build libhggraphs?**
A combination of the previous answers can be used.

   ./configure CPPFLAGS='-I/home/user/myboost -I/home/user/mygsl/include' LDFLAGS="-L/home/user/mygsl/lib"


**error while loading shared libraries: libhggraphs.so.0: cannot open
   shared object file: No such file or directory. How do I fix this problem?**
Run the following command (or put that line in your profile
   configuration file for your current shell, e.g. ~/.profile for Mac
   OS X,  ~/.bash_profile for FreeBSD, ~/.bash_rc for Ubuntu):
```
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
```
This works if your library is installed in /usr/local/lib. Otherwise
substitute that with you lib installation directory.


**Is there a way to improve the speed of the library?**
It is possible to set a different optimization level at configuration
time, using the following option: 

   ./configure CXXLAGS='-O3'

The default optimization level is -O2.


**Can I use the hggraphs library to develop new tools?**
The libhggraphs public interface is described in the hg_graphs_lib.h file that is installed in `include/hg_graphs_lib.h`. In order to link the library to your tool you need to provide the -lhggraphs option as well as the path to the lib folder containing the library at linking time.
Let's suppose that libhggraphs is installed in the default path `/usr/local`, in order to build a new tool the following operations have to be performed:

	g++ -I/usr/local/include -c my_new_tool.o my_new_tool.cpp
	g++ -o my_new_tool my_new_tool.o -L/usr/local/lib -lhggraphs

