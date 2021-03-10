
# svelte-keycloak app

This the base svelte template integrated with keycloak (open source identity and access management)

## config

    npm install

    configured keycloak client (protocol: openid-connect, access type: public )

    update your keycloak client redirect URIs and Web origins to http://localhost:5000/* and http://localhost:5000/
       
    save keycloak.json to /public (get json contents from your keycloak admin console.  client -> installation tab -> Keycloak OIDC json)

## run dev server

    npm run dev

    (see svelte starter template docs for more options)


## JWT token

the jwt token from keycloak is stored in the `userInfo` store under token.

your backend should validate this, either by consuming the `/protocol/openid-connect/certs` endpoint or storing the public key/cert from keycloak.