# $FreeBSD$

PORTNAME=	hpx
DISTVERSION=	1.2.1
PORTREVISION=	1
CATEGORIES=	devel

MAINTAINER=	yuri@FreeBSD.org
COMMENT=	C++ Standard Library for Parallelism and Concurrency

LICENSE=	BSL
LICENSE_FILE=	${WRKSRC}/LICENSE_1_0.txt

LIB_DEPENDS=	libboost_filesystem.so:devel/boost-libs \
		libhwloc.so:devel/hwloc

USES=		cmake compiler:c++17-lang python shebangfix
USE_GITHUB=	yes
GH_ACCOUNT=	STEllAR-GROUP
SHEBANG_FILES=	cmake/templates/hpxrun.py.in cmake/templates/hpxcxx.in python/scripts/*.py
USE_LDCONFIG=	yes

CMAKE_ON=	HPX_WITH_GENERIC_CONTEXT_COROUTINES
CMAKE_OFF=	HPX_WITH_EXAMPLES HPX_WITH_TESTS

.include <bsd.port.mk>
