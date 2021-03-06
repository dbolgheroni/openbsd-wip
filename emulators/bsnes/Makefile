# $OpenBSD: Makefile,v 1.6 2019/07/12 20:46:09 sthen Exp $

COMMENT =	multi-system Nintendo emulator

V =		113
DISTNAME =	bsnes_v$V-source
PKGNAME =	bsnes-$V

USE_WXNEEDED =	Yes

CATEGORIES =	emulators

HOMEPAGE =	https://bsnes.byuu.org/

MAINTAINER =	Anthony J. Bentley <anthony@anjbe.name>

# bsnes: GPLv3 only; libco, nall, ruby, hiro: ISC
PERMIT_PACKAGE =	Yes

WANTLIB += ${COMPILER_LIBCXX} GL SDL2 X11 Xcomposite Xcursor Xdamage
WANTLIB += Xext Xfixes Xi Xinerama Xrandr Xrender Xv atk-1.0 c
WANTLIB += cairo fontconfig freetype gdk-x11-2.0 gdk_pixbuf-2.0
WANTLIB += gio-2.0 glib-2.0 gobject-2.0 gtk-x11-2.0 gtksourceview-2.0
WANTLIB += intl m openal pango-1.0 pangocairo-1.0 pangoft2-1.0
WANTLIB += z

MASTER_SITES =	https://download.byuu.org/
EXTRACT_SUFX =	.zip

RUN_DEPENDS =	devel/desktop-file-utils
LIB_DEPENDS =	audio/openal \
		devel/sdl2 \
		x11/gtksourceview

MAKE_FLAGS =	compiler="${CXX}" \
		cflags="${CFLAGS} -x c -std=c11 -DLIBCO_MPROTECT" \
		cppflags="${CXXFLAGS} -x c++ -std=c++14 \
			-I${LOCALBASE}/include -I${X11BASE}/include" \
		build= \
		local=false \
		openmp=false

COMPILER =	base-clang ports-gcc base-gcc

USE_GMAKE =	Yes

NO_TEST =	Yes

MAKE_FILE =	GNUmakefile

pre-configure:
	${SUBST_CMD} ${WRKDIST}/nall/path.hpp

do-build:
	cd ${WRKSRC}/bsnes && env -i ${MAKE_ENV} ${MAKE_PROGRAM} \
		${MAKE_FLAGS} -f ${MAKE_FILE} ${ALL_TARGET}

do-install:
	${INSTALL_PROGRAM} ${WRKDIST}/bsnes/out/bsnes ${PREFIX}/bin
	${INSTALL_DATA_DIR} ${PREFIX}/share/applications
	${INSTALL_DATA} ${WRKSRC}/bsnes/target-bsnes/resource/bsnes.desktop \
		${PREFIX}/share/applications
	${INSTALL_DATA_DIR} ${PREFIX}/share/pixmaps
	${INSTALL_DATA} ${WRKSRC}/bsnes/target-bsnes/resource/bsnes.png \
		${PREFIX}/share/pixmaps

.include <bsd.port.mk>
