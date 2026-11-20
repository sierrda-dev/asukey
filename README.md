# asukey

Gestionnaire de mots de passe **local** pour Windows 11, chiffré de bout en bout, sans compte en ligne.

**Dernière version : 0.1.6.1** (20 novembre 2026)

- **Télécharger** : [https://sierrda-dev.github.io/coffre](https://sierrda-dev.github.io/coffre) (kit d'installation)
- **Déjà installé** (0.1.2 ou plus récent) : asukey propose les mises à jour tout seul.
- **Toutes les versions** : [Releases](https://github.com/sierrda-dev/coffre/releases) · [Journal des versions](CHANGELOG.md)

## Nouveautés de la 0.1.6.1

**Fiabilité et préparation au Microsoft Store**

**Nouvel éditeur : sierrda-dev**
- asukey est désormais signé au nom de **sierrda-dev** (certificat `CN=sierrda-dev`, paquet `sierrda-dev.asukey`). Pour Windows, c'est une nouvelle application : la mise à jour automatique depuis la 0.1.6 ne peut pas se faire, asukey te propose alors de télécharger le kit.
- **« Installer asukey » s'occupe de tout** : il installe la nouvelle version, qui reprend au premier lancement les réglages de l'ancienne (comptes, apparence, navigateurs associés, clé secrète mémorisée, synchronisation, sauvegardes, logos), puis il retire l'ancienne. Ton coffre, dans Documents, n'est pas touché. Seul **Windows Hello est à réactiver** (Réglages › Sécurité) : sa clé appartenait à l'ancienne application, asukey te le rappelle.
- La même reprise servira au passage à la version du Microsoft Store.

**Un seul fichier à télécharger**
- La version GitHub ne contient plus que le **kit** (`asukey-<version>-kit.zip`) : « Installer asukey », LISEZ-MOI et le paquet signé avec son certificat. Plus de version portable, plus d'extensions ni de guide en double : l'extension de navigateur et le guide sont dans l'application.
- **Mises à jour** : asukey télécharge lui-même ce kit, vérifie son empreinte (signée par l'éditeur dans l'annonce de version : un zip modifié est refusé), en extrait le paquet et l'installe. Windows ne met plus à jour asukey en arrière-plan ; asukey vérifie à l'ouverture et une fois par jour, comme avant.

**Remplissage plus sûr**
- asukey utilise maintenant la **liste officielle des suffixes publics** (publicsuffix.org, plus de 10 000 règles) pour savoir si deux adresses sont le même site. Deux boutiques `….myshopify.com`, deux pages `….github.io`, deux sites `….co.uk` ou deux espaces `….s3.amazonaws.com` sont des sites différents : un identifiant de l'un n'est plus jamais proposé sur l'autre. Avant, seule une cinquantaine de cas étaient connus.
- L'extension de navigateur applique la même règle pour les connexions en deux pages et l'enregistrement des identifiants (elle se contentait des deux derniers morceaux de l'adresse).
- Sentinelle : un service connu en `.co.uk` ne couvre plus tous les sites `.co.uk` (2FA et passkeys disponibles).

**Sécurité**
- **Logos des sites** : asukey vérifie l'adresse réellement contactée, redirections comprises, et ne joint jamais ton réseau local (box, NAS, imprimante), même si un site y renvoie.
- **Pont de l'extension** : 32 connexions simultanées au plus, et une requête doit arriver en 10 secondes ; un programme de l'ordinateur ne peut plus l'encombrer.
- Les primitives cryptographiques écrites dans asukey (BLAKE2b, Argon2, X25519, Ed25519) sont désormais vérifiées par les vecteurs de **Project Wycheproof** (728 cas d'attaque connus) et par des centaines d'entrées aléatoires comparées à OpenSSL et hash-wasm, sur Windows comme sur Mac. Aucun écart trouvé.

**Microsoft Store**
- Politique de confidentialité complétée (synchronisation directe avec OneDrive, Google Drive et pCloud ; emplacement exact des réglages).
- Revue de conformité des fonctions sensibles (docs/STORE.md) et notes prêtes pour la certification.
- Dès que l'extension sera publiée dans les boutiques des navigateurs, « Installer l'extension » y mènera directement (plus de mode développeur).

**Qualité**
- 18 nouveaux tests du cœur (112 au total, avec plus de 1 300 vecteurs cryptographiques), plus un test de l'extension et deux du Mac ; la CI lance aussi les tests JavaScript et `swift test`.
- `tools\tests.ps1` lance tous les tests en une commande (`-E2E` pour ceux dans Chrome).
- Les numéros de version (application, extensions, VS Code, README) sont alignés automatiquement à la publication, et un test le vérifie.

## Installer

1. Télécharge `asukey-0.1.6.1-kit.zip` depuis la [dernière version](https://github.com/sierrda-dev/coffre/releases/latest).
2. Clic droit › **Extraire tout**, puis double-clic sur **Installer asukey**.
3. Windows demande d'approuver l'éditeur d'asukey une seule fois par ordinateur.

## Sécurité

Les paquets sont signés par le certificat [Coffre.cer](https://sierrda-dev.github.io/coffre/Coffre.cer) ; Windows refuse une mise à jour signée par un autre. Le site ne reçoit rien de ton coffre : l'application y lit seulement [version.json](https://sierrda-dev.github.io/coffre/version.json).

Ce dépôt contient le site de téléchargement et des mises à jour. Il est publié par `tools/release.ps1 -Publish`.
