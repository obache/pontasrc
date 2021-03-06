# $NetBSD: Makefile,v 1.3 2020/10/12 21:52:30 kim Exp $

PKGNAME=	ca-certificates-20200601
PKGREVISION=	1
DISTNAME=	${PKGNAME_NOREV:C/-([^-]*)$/_\1/}
CATEGORIES=	security
MASTER_SITES=	http://deb.debian.org/debian/pool/main/c/ca-certificates/
EXTRACT_SUFX=	.tar.xz

MAINTAINER=	pkgsrc-users@NetBSD.org
HOMEPAGE=	https://packages.debian.org/source/sid/ca-certificates
COMMENT=	Root CA certificates from the Mozilla Project
LICENSE=	gnu-gpl-v2 AND mpl-2.0

NO_CONFIGURE=		yes
PYTHON_FOR_BUILD_ONLY=	yes

USE_TOOLS=	echo:run find:run ln:run openssl:run rm:run sed:run sort:run wc:run

WRKSRC=		${WRKDIR}/${PKGNAME_NOREV}
DATADIR=	${PREFIX}/share/${PKGBASE}
DOCDIR=		${PREFIX}/share/doc/${PKGBASE}
EGDIR=		${PREFIX}/share/examples/${PKGBASE}
MANDIR=		${PREFIX}/${PKGMANDIR}/man8

# Set paths depending on whether we depend on builtin or pkgsrc
# openssl.  \todo Arguably, we should consider installing into both
# builtin and pkgsrc, if both exist, but this requires much more
# thought.
CHECK_BUILTIN.openssl=	yes
.include "../../security/openssl/builtin.mk"
CHECK_BUILTIN.openssl=	no
.if !empty(USE_BUILTIN.openssl:M[yY][eE][sS])
SSLDIR=		/etc/openssl
.else
SSLDIR=		${PKG_SYSCONFDIR}/openssl
.endif

SUBST_CLASSES=		conf paths
SUBST_MESSAGE.conf=	Adjusting configuration file.
SUBST_STAGE.conf=	post-build
SUBST_FILES.conf=	ca-certificates.conf
SUBST_SED.conf=		-e 's,^share/ca-certificates/,,'
SUBST_MESSAGE.paths=	Replacing hard-coded paths.
SUBST_STAGE.paths=	post-build
SUBST_FILES.paths=	Makefile sbin/Makefile
SUBST_FILES.paths+=	ca-certificates.conf
SUBST_FILES.paths+=	sbin/update-ca-certificates sbin/update-ca-certificates.8
SUBST_FILES.paths+=	README.pkgsrc
SUBST_SED.paths=	-e 's,/usr/sbin,${PREFIX}/sbin,g'
SUBST_SED.paths+=	-e 's,/etc/ca-certificates.conf,${PKG_SYSCONFDIR}/ca-certificates.conf,g'
SUBST_SED.paths+=	-e 's,/etc/ssl,${SSLDIR},g'
SUBST_SED.paths+=	-e 's,/usr/share/ca-certificates,${DATADIR},g'

INSTALLATION_DIRS=	sbin ${DATADIR} ${DOCDIR} ${EGDIR} ${MANDIR}

CONF_FILES=		${EGDIR}/ca-certificates.conf \
			${PKG_SYSCONFDIR}/ca-certificates.conf

pre-build:
	@${CP} ${FILESDIR}/ca-certificates.conf ${FILESDIR}/README.pkgsrc ${WRKSRC}/
	@${GREP} '^share/ca-certificates/' ${FILESDIR}/../PLIST \
	    >> ${WRKSRC}/ca-certificates.conf

post-extract:
	${MV} ${WRKDIR}/work ${WRKSRC}

post-install:
	${INSTALL_MAN} \
	    ${WRKSRC}/sbin/update-ca-certificates.8 \
	    ${DESTDIR}${MANDIR}/
	${INSTALL_DATA} \
	    ${WRKSRC}/README.pkgsrc \
	    ${WRKSRC}/debian/README.source \
	    ${WRKSRC}/debian/changelog \
	    ${DESTDIR}${DOCDIR}/
	${INSTALL_DATA} \
	    ${WRKSRC}/ca-certificates.conf \
	    ${DESTDIR}${EGDIR}/

.include "../../lang/python/tool.mk"
.include "../../mk/bsd.pkg.mk"
