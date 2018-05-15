#
#  Makefile for FastCGI development kit
#
#  $Id: Makefile.am,v 1.8 2003/11/02 21:42:47 robs Exp $
#
ACLOCAL_AMFLAGS = -I m4

SUBDIRS = src include

if ENABLE_EXAMPLES
SUBDIRS += examples
endif

if ENABLE_CGI
SUBDIRS += cgi-fcgi
endif

include_HEADERS = include/fcgi_config.h

pkgconfigdir = @pkgconfigdir@
pkgconfig_DATA = fcgi.pc \
                 fcgi++.pc

EXTRA_DIST = LICENSE                    \
	     ChangeLog.md               \
             cgi-fcgi/cgi-fcgi.mak      \
             examples/authorizer.mak    \
             examples/echo.mak          \
             examples/echox.mak         \
             examples/size.mak          \
             examples/echo-cpp.mak      \
             src/libfcgi.mak            \
             images/aplib-hd.gif        \
             images/divider.gif         \
             images/fcgi-hd.gif         \
             images/mail-hd.gif         \
             images/navbar.gif          \
             images/serv-hd.gif         \
             images/words-hd.gif        \
             include/fcgi_config_x86.h  \
             src/os_unix.c              \
             src/os_win32.c             \
             doc/FCGI_Accept.3          \
             doc/FCGI_Finish.3          \
             doc/FCGI_SetExitStatus.3   \
             doc/FCGI_StartFilterData.3 \
             doc/cgi-fcgi.1             \
             doc/fcgi-devel-kit.htm     \
             doc/fcgi-java.htm          \
             doc/fcgi-perf.htm          \
             doc/fcgi-perl.htm          \
             doc/fcgi-spec.html         \
             doc/fcgi-tcl.htm           \
             doc/omi-logo.gif           \
             doc/overview.html          \
             doc/www5-api-workshop.html \
             doc/fastcgi-prog-guide/ap_guida.htm        \
             doc/fastcgi-prog-guide/ap_guide.htm        \
             doc/fastcgi-prog-guide/apaman.htm          \
             doc/fastcgi-prog-guide/ch1inta1.gif        \
             doc/fastcgi-prog-guide/ch1intra.gif        \
             doc/fastcgi-prog-guide/ch1intro.htm        \
             doc/fastcgi-prog-guide/ch2c.htm            \
             doc/fastcgi-prog-guide/ch3perl.htm         \
             doc/fastcgi-prog-guide/ch4tcl.htm          \
             doc/fastcgi-prog-guide/cover.htm           \
             doc/fastcgi-prog-guide/covera.gif          \
             doc/fastcgi-whitepaper/fastcgi.htm         \
             doc/fastcgi-whitepaper/img00001.gif        \
             doc/fastcgi-whitepaper/img00002.gif        \
             doc/fastcgi-whitepaper/img00003.gif


MD5 = md5sum
md5-dist:
	@for file in $(DIST_ARCHIVES); do	\
		$(MD5) $$file > ../$$file.md5;	\
		mv $$file ../;			\
	done

## Check if tagged in git
release-hook:
	if [ ! `git tag | grep $(PACKAGE_VERSION)` ]; then				\
		echo;									\
		printf "\e[1m\e[41mCannot find release tag $(PACKAGE_VERSION)\e[0m\n";	\
		printf "\e[1m\e[5mDo release anyway?\e[0m "; read yorn;			\
		if [ "$$yorn" != "y" -a "$$yorn" != "Y" ]; then				\
			printf "OK, aborting release.\n";				\
			exit 1;								\
		fi;									\
		echo;									\
	else										\
		echo;									\
		printf "\e[1m\e[42mFound GIT release tag $(PACKAGE_VERSION)\e[0m\n";	\
		printf "\e[1m\e[44m>>Remember to push tags!\e[0m\n";			\
		echo;									\
	fi

## Target to run when building a release
## distcheck <-- does not work atm., wrong search path for source/header files
release: distcheck release-hook md5-dist
	@echo
	@echo "Resulting release files:"
	@echo "================================================================="
	@for file in $(DIST_ARCHIVES); do						\
		printf "$$file    \tDistribution tarball\n";				\
		printf "$$file.md5\t"; cat ../$$file.md5 | cut -f1 -d' ';		\
	done
