
# SSO Keycloak avec WordPress

Cet article va décrire comment mettre en place du SSO avec un serveur keycloak. Un début avant de continuer serait de lire Du SSO avec keycloak qui vous permettra d’avoir un serveur keycloak opérationnel. On supposera dans la suite de cet article que

votre serveur keycloak est accessible via : https://auth.exemple.fr
votre serveur wordpress est accessible via https://www.exemple.fr

## Docs

- https://home.cleon.re/sso-keycloak-avec-wordpress/

## WordPress
Nous allons indiquer a WordPress d’utiliser keycloak comme fournisseur d’identité. Dans cet article je vais utiliser le protocol openid-connect comme moyen de fédération.

Pour cela il vous faudra installer une extension a WordPress pour mettre en oeuvre openid-connect. OpenID Connect Generic Client fera très bien l’affaire. Installer donc cet extension et rendez-vous dans votre tableau de bord / Réglages / OpenId Connect Client ( /wp-admin/options-general.php?page=openid-connect-generic-settings )

Client ID	wordpress-client-id
Client Secret Key	ccd3ad80-e62f-46ca-aafa-4da3405e64e8
OpenID Scope	openid
Login Endpoint URL	https://auth.exemple.fr/auth/realms/master/protocol/openid-connect/auth
Userinfo Endpoint URL	https://auth.exemple.fr/auth/realms/master/protocol/openid-connect/userinfo
Token Validation Endpoint URL	https://auth.exemple.fr/auth/realms/master/protocol/openid-connect/token
End Session Endpoint URL	https://auth.exemple.fr/auth/realms/master/protocol/openid-connect/logout
Si vous souhaitez que les utilisateurs existants soient reconnus et liés aux comptes existants, via leur email. Veillez a cocher la case

Link Existing Users

If a WordPress account already exists with the same identity as a newly-authenticated user over OpenID Connect, login as that user instead of generating an error.

Par défaut le lien se fera par l’adresse email, si vous souhaitez une fédération via le login, veillez à cocher la case

Identify with User Name

If checked, the user’s identity will be determined by the user name instead of the email address.

Keycloak
Connectez vous en admin sur votre console keycloak
Allez dans le menu Clients
Cliquez sur Create
Renseignez les paramètres suivants
Client ID	wordpress-client-id
Client Protocol	openid-connect
Enregistrez
La page de configuration du client s’affiche
Dans Valid redirect URIs, veuillez ajouter l’adresse de votre wordpress ( dans notre cas https://www.exemple.fr/* )
Enregistrez les modifications
Lors de l’accès à la page de connexion de wordpress, vous allez disposer sur la mire d’authentification de wordpress un bouton vous permettant de vous connecter avec keycloak
