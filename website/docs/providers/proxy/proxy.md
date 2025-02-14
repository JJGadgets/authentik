---
title: Overview
---

The proxy outpost sets the following user-specific headers:

- X-authentik-username: `akadmin`

    The username of the currently logged in user

- X-authentik-groups: `foo|bar|baz`

    The groups the user is member of, separated by a pipe

- X-authentik-email: `root@localhost`

    The email address of the currently logged in user

- X-authentik-name: `authentik Default Admin`

    Full name of the current user

- X-authentik-uid: `900347b8a29876b45ca6f75722635ecfedf0e931c6022e3a29a8aa13fb5516fb`

    The hashed identifier of the currently logged in user.

Additionally, you can set `additionalHeaders` on groups or users to set additional headers.

If you enable *Set HTTP-Basic Authentication* option, the HTTP Authorization header is being set.

Besides these user-specific headers, some application specific headers are also set:

- X-authentik-meta-outpost: `authentik Embedded Outpost`

    The authentik outpost's name.

- X-authentik-meta-provider: `test`

    The authentik provider's name.

- X-authentik-meta-app: `test`

    The authentik application's slug.

- X-authentik-meta-version: `authentik-outpost@1.2.3 (build=tagged)`

    The authentik outpost's version.

## HTTPS

The outpost listens on both 9000 for HTTP and 9443 for HTTPS.

:::info
If your upstream host is HTTPS, and you're not using forward auth, you need to access the outpost over HTTPS too.
:::

## Logging out

Login is done automatically when you visit the domain without a valid cookie.

When using single-application mode, navigate to `app.domain.tld/akprox/sign_out`.

When using domain-level mode, navigate to `auth.domain.tld/akprox/sign_out`, where auth.domain.tld is the external host configured for the provider.

To log out, navigate to `/akprox/sign_out`.

## Allowing unauthenticated requests

To allow un-authenticated requests to certain paths/URLs, you can use the *Unauthenticated URLs* / *Unauthenticated Paths* field.

Each new line is interpreted as a regular expression, and is compiled and checked using the standard Golang regex parser.

The behaviour of this field changes depending on which mode you're in.

### Proxy and Forward auth (single application)

In this mode, the regular expressions are matched against the Request's Path.

### Forward auth (domain level)

In this mode, the regular expressions are matched against the Request's full URL.
