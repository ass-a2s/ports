# Created by: vanilla@
# $FreeBSD$

PORTNAME=	libzdb
PORTVERSION=	3.2
CATEGORIES=	databases
MASTER_SITES=	https://www.tildeslash.com/libzdb/dist/

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Thread-safe connection pool library

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/COPYING

USES=		gmake libtool localbase pathfix

GNU_CONFIGURE=	yes
INSTALL_TARGET=	install-strip
USE_LDCONFIG=	yes

OPTIONS_DEFINE=		SSL
OPTIONS_DEFAULT=	MYSQL PGSQL SQLITE SSL
OPTIONS_MULTI=		DB
OPTIONS_MULTI_DB=	MYSQL PGSQL SQLITE

MYSQL_CONFIGURE_WITH=	mysql=${LOCALBASE}/bin/mysql_config
MYSQL_USES=		mysql
PGSQL_CONFIGURE_WITH=	postgresql=${LOCALBASE}/bin/pg_config
PGSQL_USES=		pgsql
SQLITE_CONFIGURE_WITH=	sqlite=${LOCALBASE}
SQLITE_USES=		sqlite
SSL_CONFIGURE_ENABLE=	openssl=${OPENSSLBASE}
SSL_USES=		ssl

.include <bsd.port.mk>
