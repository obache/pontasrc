# $NetBSD$

DISTNAME=	TracAccountManager-0.5.0
PKGNAME=	${DISTNAME:S/Trac/trac-plugins-/}
CATEGORIES=	www
MASTER_SITES=	${MASTER_SITE_PYPI:=T/TracAccountManager/}

HOMEPAGE=	http://trac-hacks.org/wiki/AccountManagerPlugin
COMMENT=	User account management plugin for Trac
LICENSE=	modified-bsd

DEPENDS+=	trac>=0.12:../../www/trac
DEPENDS+=	${PYPKGPREFIX}-babel>=0.9.5:../../devel/py-babel

.include "../../lang/python/egg.mk"
.include "../../mk/bsd.pkg.mk"
