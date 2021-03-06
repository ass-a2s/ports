# Created by: Alex Dupre <ale@FreeBSD.org>
# $FreeBSD$

PORTNAME=	quantis
DISTVERSION=	v18.03.08
PORTREVISION=	4
CATEGORIES=	security devel java
MASTER_SITES=	https://www.idquantique.com/wordpress/wp-content/uploads/
DISTNAME=	Quantis-${DISTVERSION}

MAINTAINER=	ale@FreeBSD.org
COMMENT=	Libraries and utilities to access Quantis devices

LICENSE=	BSD3CLAUSE GPLv2
LICENSE_COMB=	dual
LICENSE_FILE_BSD3CLAUSE=${WRKSRC}/../License.txt

BROKEN=		does not build
BROKEN_aarch64=		fails to build: Could not find JNI (missing: JAVA_AWT_LIBRARY JAVA_JVM_LIBRARY)
BROKEN_armv6=		fails to build: Could not find JNI (missing: JAVA_AWT_LIBRARY JAVA_JVM_LIBRARY)
BROKEN_armv7=		fails to build: Could not find JNI (missing: JAVA_AWT_LIBRARY JAVA_JVM_LIBRARY)
DEPRECATED=	Broken for more than 6 months
EXPIRATION_DATE=	2019-05-08

USES=		cmake compiler:c++11-lang zip:infozip

OPTIONS_DEFINE=	PCI USB JAVA COMPAT TOOL DOCS EXAMPLES
OPTIONS_DEFAULT=PCI USB JAVA TOOL
NO_OPTIONS_SORT=yes

PCI_DESC=	Enable Quantis PCI support
USB_DESC=	Enable Quantis USB support
JAVA_DESC=	Enable Java support
COMPAT_DESC=	Build API v1 compatibility libraries
TOOL_DESC=	Build EasyQuantis application

EXTRACT_BEFORE_ARGS=	-aqo
USE_LDCONFIG=	yes
SUB_FILES=	pkg-message

WRKSRC=		${WRKDIR}/Quantis-${DISTVERSION}/Libs-Apps

KMODDIR?=	/boot/modules

PORTDOCS=	*
PORTEXAMPLES=	*

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MPCI}
RUN_DEPENDS+=	${KMODDIR}/quantis.ko:security/quantis-kmod
.else
CMAKE_ARGS+=	-DDISABLE_QUANTIS_PCI=1
.endif

.if ! ${PORT_OPTIONS:MUSB}
CMAKE_ARGS+=	-DDISABLE_QUANTIS_USB=1
PKGMESSAGE=	${PKGDIR}/notexistent
.endif

.if ${PORT_OPTIONS:MJAVA}
USE_JAVA=	yes
JAVA_VERSION=	1.6+
JAVA_OS=	native
.else
CMAKE_ARGS+=	-DDISABLE_QUANTIS_JAVA=1
.endif

.if ${PORT_OPTIONS:MCOMPAT}
CMAKE_ARGS+=	-DENABLE_QUANTIS_COMPAT=1

PLIST_SUB+=	COMPAT=""
.else
PLIST_SUB+=	COMPAT="@comment "
.endif

.if ${PORT_OPTIONS:MTOOL}
BUILD_DEPENDS+=	${LOCALBASE}/lib/libboost_date_time.a:devel/boost-libs
CXXFLAGS+=	-I${LOCALBASE}/include

CMAKE_ARGS+=	-DDISABLE_EASYQUANTIS_GUI=1

PLIST_SUB+=	TOOL=""
.else
CMAKE_ARGS+=	-DDISABLE_EASYQUANTIS=1

PLIST_SUB+=	TOOL="@comment "
.endif

post-patch:
	@${REINPLACE_CMD} '/  if(CMAKE_COMPILER_IS_GNU/s/)/ MATCHES "0")/' \
		${WRKSRC}/CMake/CompilersFlags.cmake

post-install:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/../*.txt ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/../User_Manual.pdf ${STAGEDIR}${DOCSDIR}
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	@(cd ${WRKSRC}/../Samples; ${COPYTREE_SHARE} . ${STAGEDIR}${EXAMPLESDIR} "-not -empty")
.if ${PORT_OPTIONS:MUSB}
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}/devd
	${INSTALL_DATA} ${FILESDIR}/quantis.conf ${STAGEDIR}${EXAMPLESDIR}/devd
.endif

.include <bsd.port.mk>
