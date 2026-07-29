<div align="center">

# Noliae Account

### Espace compte sécurisé — Nolc MVC

[![CI](https://github.com/Noliae-France/Noliae-Account/actions/workflows/ci.yml/badge.svg)](https://github.com/Noliae-France/Noliae-Account/actions/workflows/ci.yml)

</div>

Application de compte pour **`account.noliae.com`** : informations
personnelles, sécurité et préférences. Le rendu est Nolc/.nhtml et le design
reprend l’interface Noliae (topbar Encre, sidebar, Vermillon et cartes).

## Autorisation

Le reverse proxy doit router `/v1/*` vers NolCore. Ainsi, toute lecture ou
modification de profil passe par la validation réelle de `nol_session` dans le
Core : signature HMAC, IP, e-mail, expiration et révocation PostgreSQL.

L’UI ne fait jamais confiance à la simple présence d’un cookie pour autoriser
une action sensible. Pour utiliser IA, le même mécanisme Core protège
`/v1/ia/*` : sans session valide, la réponse reste `401 Unauthorized`.

## Développement et livraison

```sh
nolc nhtml views/account.nhtml
nolc check main.nol
docker build -t noliae-account .
```

Le pipeline GitHub Actions compile le binaire, smoke-teste `/api/health` puis
publie `ghcr.io/noliae-france/noliae-account:main`.
