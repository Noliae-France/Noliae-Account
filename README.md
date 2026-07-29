# Noliae Account

Espace compte Nolc/.nhtml pour `account.noliae.com`. Les changements de profil
et de mot de passe sont dirigés vers les routes protégées NolCore. L’Ingress
doit proxyfier `/v1/*` vers NolCore afin que celui-ci valide le cookie `nol_session`.
