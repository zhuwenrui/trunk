###############
Installation
###############

Yade can be installed from packages (precompiled binaries) or source code. 
The choice depends on what you need: if you don't plan to modify Yade itself, 
package installation is easier. In the contrary case, you must download and 
install source code.

Since 2011 Yade persists in Ubuntu and Debian main repositories.
There are only stable releases are placed.
Please, consider installing them::

	sudo apt-get install yade

Packages
----------

Packages from Launchpad PPA service (package personal archive) are 
provided for all currently supported Ubuntu versions for 
`stable <https://launchpad.net/~yade-pkg/+archive/stable>`_ and 
`daily <https://launchpad.net/~yade-pkg/+archive/snapshots>`_ releases.
``yade-daily`` is a automatically daily (if there were some commtis during
the previous days) geenrated package, which includes all the newly added 
features. To install version from PPA, run the following:

* For stable releases::

	sudo add-apt-repository ppa:yade-pkg/stable       # for stable releases 
	sudo add-apt-repository ppa:yade-users/external   # optional (updates of other packages)
	sudo apt-get update
	sudo apt-get install yade

* For latest builds from trunk::

	sudo add-apt-repository ppa:yade-pkg/snapshots    # for latest ddaily (mostly) releases 
	sudo apt-get update
	sudo apt-get install yade-daily

After you added whether stable or snapshot PPAs, you will get automatically
the updates of the package, when they arrive the PPA.

More detailed instructions are available at the corresponding pages of 
ppa`s (links above).

Source code
------------

Installation from source code is reasonable, when you want to add or 
modify constitutive laws, engines or functions... Installing the latest 
trunk version allows one to use newly added features, which are not yet 
available in packaged versions. 

Download
^^^^^^^^^^

If you want to install from source, you can install either a release 
(numbered version, which is frozen) or the current developement version 
(updated by the developers frequently). You should download the development 
version (called ``trunk``) if you want to modify the source code, as you 
might encounter problems that will be fixed by the developers. Release 
version will not be modified (except for updates due to critical and 
easy-to-fix bugs), but they are in a more stabilized state that trunk 
generally.

#. Releases can be downloaded from the `download page <https://launchpad.net/yade/+download>`_, as compressed archive. Uncompressing the archive gives you a directory with the sources.
#. developement version (trunk) can be obtained from the `code repository <https://github.com/yade/>`_ at github.

We use `GIT <http://git-scm.com/>`_ (the ``git`` command) for code 
management (install the ``git`` package in your distribution)::

		git clone git://github.com/yade/trunk.git

will download the whole code repository of ``trunk``. Check out `Yade on github
<https://www.yade-dem.org/wiki/Yade_on_github>`_ wiki page for more.
   
For those behind firewall, you can download `any revision  <https://www.yade-dem.org/source/>`_ of the repository as compressed archive.

Release and trunk sources are compiled in the same way.

Prerequisities
^^^^^^^^^^^^^^^

Yade relies on a number of external software to run; its installation is checked before the compilation starts. 

* `cmake <http://www.cmake.org/>`_ build system
* `gcc <http://www.gcc.gnu.org>`_ compiler (g++); other compilers will not work; you need g++>=4.2 for openMP support
* `boost <http://www.boost.org/>`_ 1.35 or later
* `qt4 <http://www.qt.nokia.com>`_ library
* `freeglut3 <http://freeglut.sourceforge.net>`_
* `libQGLViewer <http://www.libqglviewer.com>`_
* `python <http://www.python.org>`_, `numpy <http://numpy.scipy.org>`_, `ipython <http://ipython.scipy.org>`_
* `matplotlib <http://matplotlib.sf.net>`_
* `eigen3 <http://eigen.tuxfamily.org>`_ algebra library
* `gdb <http://www.gnu.org/software/gdb>`_ debugger
* `sqlite3 <http://www.sqlite.org>`_ database engine
* `Loki <http://loki-lib.sf.net>`_ library
* `VTK <http://www.vtk.org/>`_ library (optional but recommended)

Most of the list above is very likely already packaged for your distribution. 
The following commands have to be executed in command line of corresponding 
distributions. Just copy&paste to the terminal. To perform commands you 
should have root privileges

	* **Ubuntu**, **Debian** and their derivatives::

		sudo apt-get install cmake git freeglut3-dev libloki-dev \
		libboost-date-time-dev libboost-filesystem-dev libboost-thread-dev \
		libboost-program-options-dev \
		libboost-regex-dev fakeroot dpkg-dev build-essential g++ \
		libboost-iostreams-dev python-dev libboost-python-dev ipython \
		python-matplotlib libsqlite3-dev python-numpy python-tk gnuplot doxygen \
		libgts-dev python-pygraphviz libvtk5-dev python-scientific libeigen3-dev \
		binutils-gold python-xlib python-qt4 pyqt4-dev-tools \
		gtk2-engines-pixbuf \
		libqglviewer-qt4-dev python-imaging libjs-jquery python-sphinx python-git python-bibtex \
		libxmu-dev libxi-dev libgmp3-dev libcgal-dev

	* **Fedora**::

		yum install cmake qt3-devel freeglut-devel boost-devel boost-date-time \
		boost-filesystem boost-thread boost-regex fakeroot gcc gcc-c++ boost-iostreams \
		python-devel boost-python ipython python-matplotlib \
		sqlite-devel python-numeric ScientificPython-tk gnuplot doxygen gts-devel \
		graphviz-python vtk-devel ScientificPython bzr bzrtools eigen2-devel libQGLViewer-devel \
		loki-lib-devel python-xlib PyQt4 PyQt4-devel python-imaging python-sphinx python-bibtex


Compilation
^^^^^^^^^^^

You should create a separate build-place-folder, where Yade will be configured 
and where the source code will be compiled. Then inside this build-directory you
should start cmake to configure the compilation process::

	cmake -DINSTALL_PREFIX=/path/to/installfolder /path/to/sources

Additional options can be configured in the same line with the following 
syntax::

	cmake -DOPTION1=VALUE1 -DOPTION2=VALUE2
	
The following options are available:
	
	* INSTALL_PREFIX: absolute path to install Yade (/usr/local by default)
	* LIBRARY_OUTPUT_PATH: path to install libraries (lib by default)
	* DEBUG: compile in debug-mode (OFF by default)
	* CMAKE_VERBOSE_MAKEFILE: output additional information during compiling (OFF by default)
	* SUFFIX: suffix, added after binary-names (version number by default)
	* NOSUFFIX: do not add a suffix after binary-name (OFF by default)
	* YADE_VERSION: explicitely set version number (is defined from git-directory by default)
	* ENABLE_GUI: enable GUI option (ON by default)
	* ENABLE_CGAL: enable CGAL option (ON by default)
	* ENABLE_VTK: enable VTK-export option (ON by default)
	* ENABLE_OPENMP: enable OpenMP-parallelizing option (ON by default)
	* ENABLE_GTS: enable GTS-option (ON by default)
	* ENABLE_GL2PS: enable GL2PS-option (ON by default)
	* runtimePREFIX: used for packaging, when install directory is not the same is runtime directory (/usr/local by default)
	* CHUNKSIZE: used, if you want several sources to be compiled at once. Increases compilation speed and RAM-consumption during it (1 by default).

For using an extended parameters of cmake, please, follow the corresponding
documentation on cmake-webpage. 

If the compilation is finished without errors, you will see all enabled 
and disabled options. Then start the standard the compilation process::

	make

Installing performs with the following command::

	make install

The compilation process can take a long time, be patient. An additional
parameter on many cores systems ``-j`` can be added to decrease compilation time
and split the compilation on many cores. For example, on 4-core machines
it would be reasonable to set the parameter ``-j4``. Note, the Yade requires
approximately 2GB/core for compilation, otherwise the swap-file will be used
and a compilation time dramatically increases.
