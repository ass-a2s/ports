# Created by: Ju Pengfei <jupengfei@gmail.com>
# $FreeBSD$

PORTNAME=	apvlv
PORTVERSION=	0.1.4
PORTREVISION=	10
CATEGORIES=	graphics
MASTER_SITES=	GHC
DISTNAME=	${PORTNAME}-${PORTVERSION}-Source

MAINTAINER=	xors@mailup.net
COMMENT=	PDF/DJVU Viewer that behaves like Vim

LICENSE=	GPLv2

BROKEN=		fails to build
DEPRECATED=	Broken for more than 6 months
EXPIRATION_DATE=	2019-05-08

LIB_DEPENDS=	libpoppler-glib.so:graphics/poppler-glib

USE_GNOME=	gtk20
USES=		cmake:insource pkgconfig
USE_GITHUB=	yes
GH_ACCOUNT=	naihe2010
CMAKE_ARGS+=	-DSYSCONFDIR=${PREFIX}/etc \
		-DMANDIR=${MANPREFIX}/man \
		-DDOCDIR=${DOCSDIR} \
		-DAPVLV_WITH_UMD=OFF \
		-DAPVLV_WITH_HTML=OFF \
		-DAPVLV_WITH_TXT=ON
CFLAGS+=	-pthread
LDFLAGS+=	-pthread
WRKSRC=		${WRKDIR}/${DISTNAME}

OPTIONS_DEFINE=	DJVU

DJVU_DESC=	DjVu document support

DJVU_CMAKE_ON=	-DAPVLV_WITH_DJVU=ON
DJVU_CMAKE_OFF=	-DAPVLV_WITH_DJVU=OFF
DJVU_LIB_DEPENDS=	libdjvulibre.so:graphics/djvulibre

.include <bsd.port.mk>
