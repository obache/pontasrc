# $NetBSD: Makefile,v 1.16 2019/11/02 16:25:22 rillig Exp $

DISTNAME=		jchkmail-1.3.1a
PKGREVISION=		2
CATEGORIES=		mail
# old site, dead
#MASTER_SITES=		http://j-chkmail.ensmp.fr/download/
# new site, only has 2.6.1 or newer
#MASTER_SITES=		http://foss.jose-marcio.org/download/

MAINTAINER=		pkgsrc-users@NetBSD.org
HOMEPAGE=		http://foss.jose-marcio.org/wiki/doku.php
COMMENT=		Behavior-based virus and spam milter for Sendmail

USE_PKGLOCALEDIR=	yes
GNU_CONFIGURE=		yes

CONFIGURE_ARGS+=	--with-rc-dir=${PREFIX}/share/examples/rc.d	\
			--with-conf-dir=${PKG_SYSCONFDIR:Q}

EGDIR=				${PREFIX}/share/examples/jchkmail
PKG_SYSCONFSUBDIR=		jchkmail
CONF_FILES+=			${EGDIR}/j-chkmail.cf ${PKG_SYSCONFDIR}/j-chkmail.cf
CONF_FILES+=			${EGDIR}/j-local-users ${PKG_SYSCONFDIR}/j-local-users
CONF_FILES+=			${EGDIR}/j-error-msg ${PKG_SYSCONFDIR}/j-error-msg
CONF_FILES+=			${EGDIR}/j-nets ${PKG_SYSCONFDIR}/j-nets
CONF_FILES+=			${EGDIR}/j-host-access ${PKG_SYSCONFDIR}/j-host-access
CONF_FILES+=			${EGDIR}/j-user-access ${PKG_SYSCONFDIR}/j-user-access
CONF_FILES+=			${EGDIR}/j-regex ${PKG_SYSCONFDIR}/j-regex
RCD_SCRIPTS=			jchkmail
RCD_SCRIPT_SRC.jchkmail=	${WRKSRC}/bin/jchkmail.init

PTHREAD_AUTO_VARS=	yes

INSTALLATION_DIRS=	share/examples/rc.d

OWN_DIRS_PERMS+=	/var/spool/jchkmail smmsp smmsp 750 \
			/var/jchkmail  smmsp smmsp 755

.include "../../mail/libmilter/buildlink3.mk"
.include "../../mk/pthread.buildlink3.mk"
.include "../../mk/bsd.pkg.mk"
