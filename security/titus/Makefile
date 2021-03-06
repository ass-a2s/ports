# Created by: Mark Felder <feld@FreeBSD.org>
# $FreeBSD$

PORTNAME=	titus
PORTVERSION=	0.3
PORTREVISION=	4
CATEGORIES=	security

MAINTAINER=	feld@FreeBSD.org
COMMENT=	TLS/SSL proxy server

LICENSE=	MIT

USES=		compiler:c++11-lang ssl
USE_RC_SUBR=	titus

USE_GITHUB=	yes
GH_ACCOUNT=	AGWA

USERS=		titus titus-keys
GROUPS=		nogroup

MAKE_ENV+=	MANDIR=${MANPREFIX}/man
CFLAGS+=	-I${OPENSSLINC}
LDFLAGS+=	-L${OPENSSLLIB}

.include <bsd.port.pre.mk>

.if ${SSL_DEFAULT} == base
BROKEN_FreeBSD_12=	member access into incomplete type 'dh_st'
BROKEN_FreeBSD_13=	member access into incomplete type 'dh_st'
.endif

post-patch:
	${REINPLACE_CMD} 's|/var/lib/titus/empty|/var/empty|' ${WRKSRC}/titus.conf.example

post-install:
	${INSTALL_DATA} ${WRKSRC}/titus.conf.example ${STAGEDIR}${PREFIX}/etc/titus.conf.sample

.include <bsd.port.post.mk>
