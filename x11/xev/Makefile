# $FreeBSD$

PORTNAME=	xev
PORTVERSION=	1.2.3
CATEGORIES=	x11

MAINTAINER=	x11@FreeBSD.org
COMMENT=	Print contents of X events

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/COPYING

USE_HARDENING=	safestack

XORG_CAT=	app
USE_XORG=	x11 xrandr

PLIST_FILES=	bin/xev man/man1/xev.1.gz

.include <bsd.port.mk>
