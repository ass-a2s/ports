# Created by: Antoine Brodin <antoine@FreeBSD.org>
# $FreeBSD$

PORTNAME=	dosage
PORTVERSION=	2.15
PORTREVISION=	1
CATEGORIES=	deskutils python
MASTER_SITES=	CHEESESHOP

MAINTAINER=	antoine@FreeBSD.org
COMMENT=	Application to keep a local mirror of web comics

LICENSE=	MIT

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}requests>0:www/py-requests@${PY_FLAVOR}

USES=		python
USE_PYTHON=	distutils autoplist concurrent optsuffix

post-patch:
	@${REINPLACE_CMD} 's|share/man/man1|man/man1|' ${WRKSRC}/setup.py

.include <bsd.port.mk>
