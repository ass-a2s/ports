# $FreeBSD$

PORTNAME=	media-driver
DISTVERSIONPREFIX=	intel-media-
DISTVERSION=	19.1.pre3-6
DISTVERSIONSUFFIX=	-g42f6f231
CATEGORIES=	multimedia
PKGNAMEPREFIX=	libva-intel-

PATCH_SITES=	https://github.com/${GH_ACCOUNT}/${GH_PROJECT}/commit/
PATCHFILES=	95549679029d.patch:-p1

MAINTAINER=	jbeich@FreeBSD.org
COMMENT=	VAAPI driver for Intel HD 5000 (Gen8) or newer

LICENSE=	MIT BSD3CLAUSE
LICENSE_COMB=	multi
LICENSE_FILE=	${WRKSRC}/LICENSE.md

ONLY_FOR_ARCHS=	amd64 i386
ONLY_FOR_ARCHS_REASON=	Only Intel GPUs on x86 are supported

BUILD_DEPENDS=	gmmlib>=${PORTVERSION:C/([^.]*\.[^.]).*/\1/}:multimedia/gmmlib \
		libva>=2.4.0:multimedia/libva
LIB_DEPENDS=	libpciaccess.so:devel/libpciaccess \
		libigdgmm.so:multimedia/gmmlib \
		libva.so:multimedia/libva

USES=		cmake compiler:c++11-lib localbase pkgconfig
USE_GITHUB=	yes
GH_ACCOUNT=	intel
ARCH_SUFX=	${ARCH:S/i386/32/:S/amd//:S/x86_//}
CMAKE_OFF=	MEDIA_BUILD_FATAL_WARNINGS BUILD_CMRTLIB
CMAKE_ARGS=	-DBUILD_TYPE:STRING="${CMAKE_BUILD_TYPE}" \
		-DARCH:STRING="${ARCH_SUFX}" \
		-DUFO_MARCH:STRING="${CPUTYPE}"
PLIST_FILES=	lib/dri/iHD_drv_video.so

OPTIONS_DEFINE=	TEST X11
OPTIONS_DEFAULT=X11

# XXX Unbundle googletest
TEST_CMAKE_BOOL=	MEDIA_RUN_TEST_SUITE
TEST_TEST_TARGET=	RunULT

X11_LIB_DEPENDS=	libva-x11.so:multimedia/libva

post-patch:
	@${REINPLACE_CMD} -e '/-D__linux__/d' \
		${WRKSRC}/media_driver/cmake/linux/media_compile_flags_linux.cmake
	@if [ ${CHOSEN_COMPILER_TYPE} != gcc ]; then \
		${REINPLACE_CMD} -i .gcc.bak '/-fno-tree-pre/d' \
			${WRKSRC}/media_driver/cmake/linux/media_compile_flags_linux.cmake; \
	fi
# Silence -Wmacro-redefined
	@${REINPLACE_CMD} -e '/__fastcall/d' \
		${WRKSRC}/media_driver/linux/common/cm/cm_mem_os.h

post-patch-X11-off:
	@${REINPLACE_CMD} -i .nox11 '/find_package.*X11/d' \
		${WRKSRC}/media_driver/media_top_cmake.cmake

.include <bsd.port.mk>
