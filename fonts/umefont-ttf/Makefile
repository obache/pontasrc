# $NetBSD: Makefile,v 1.62 2020/11/25 15:38:50 ryoon Exp $
#

DISTNAME=	umefont_670
PKGNAME=	${DISTNAME:S/_/-ttf-0./}
CATEGORIES=	fonts japanese
MASTER_SITES=	${MASTER_SITE_OSDN:=ume-font/22212/}
EXTRACT_SUFX=	.tar.xz

MAINTAINER=	ryoon@NetBSD.org
HOMEPAGE=	http://osdn.jp/projects/ume-font/wiki/FrontPage
COMMENT=	Ume 18 Japanese fonts (Mincho and Gothic)
LICENSE=	mplusfont

WRKSRC=		${WRKDIR}/${DISTNAME:C/([a-z]+)-//}

CONFLICTS=	umefont<=0.421
SUPERSEDES=	umefont<=0.421

NO_CONFIGURE=	yes
NO_BUILD=	yes

INSTALLATION_DIRS+=	${PREFIX}/share/doc/${PKGBASE}

do-install:
	${INSTALL_DATA} ${WRKSRC}/license.html ${DESTDIR}${PREFIX}/share/doc/${PKGBASE}

.include "../../mk/fonts.mk"
.include "../../mk/bsd.pkg.mk"
