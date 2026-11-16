# Coffre

Gestionnaire de mots de passe **local** pour Windows 11 et macOS, chiffré de bout en bout, sans compte en ligne.

**Dernière version : 0.1.5** (16 novembre 2026)

- **Télécharger** : [https://sierrda-dev.github.io/coffre](https://sierrda-dev.github.io/coffre) (kit d'installation et version portable)
- **Déjà installé** (0.1.2 ou plus récent) : Coffre propose les mises à jour tout seul.
- **Toutes les versions** : [Releases](https://github.com/sierrda-dev/coffre/releases) · [Journal des versions](CHANGELOG.md)

## Nouveautés de la 0.1.5

**Sécurité des données**
- **Mises à jour signées** : l'annonce de chaque version (version.json) est signée avec une clé gardée sur le PC de publication, et contient l'empreinte de chaque fichier publié. Coffre refuse toute mise à jour dont la signature ne correspond pas : un compte GitHub piraté ne suffirait plus à diffuser un faux Coffre. Sur Mac, le fichier téléchargé est en plus vérifié avant d'être ouvert.
- **Protection contre les anciennes copies** : chaque appareil retient la version la plus récente de ton coffre qu'il a vue. Si le fichier est remplacé par une copie plus ancienne (dossier synchronisé compromis, historique de OneDrive…), Coffre prévient et ne l'ouvre qu'avec ton accord. Une ancienne copie ne peut plus remettre en place un ancien mot de passe maître lors de la synchronisation. Restaurer une sauvegarde depuis les réglages ne déclenche pas l'alerte.
- **Mot de passe maître mieux protégé** : la dérivation Argon2id utilise jusqu'à 256 Mio de mémoire (au lieu de 64), selon ce que ton appareil calcule en environ une seconde. Un vol du fichier coûte jusqu'à quatre fois plus cher à attaquer. Ton coffre est mis à niveau tout seul au prochain déverrouillage par mot de passe ; Windows Hello, Touch ID, la clé secrète et la clé de récupération continuent de fonctionner, et les autres appareils suivent automatiquement.
- **Fichiers endommagés ou piégés** : des milliers de fichiers de coffre, contenus, imports (CSV, Bitwarden, 1Password, KeePass) et annonces de version modifiés au hasard sont testés à chaque version. Les cas trouvés (base64 invalide, valeurs nulles, types inattendus) donnent maintenant un message clair au lieu d'une erreur imprévue.

**Optimisation et préparation au Microsoft Store**
- La Sentinelle est environ six fois plus rapide sur un gros coffre (5 000 éléments : 0,6 s → 0,1 s, puis quelques centièmes de seconde) : le catalogue des services est indexé une fois, l'hôte de chaque adresse et la robustesse de chaque mot de passe sont mémorisés (oubliés au verrouillage).
- La liste ne se recrée plus quand seul le contenu d'éléments change (favori, renommage sans changement d'ordre) : seules les lignes visibles sont redessinées.
- Les rubriques des réglages déjà ouvertes s'affichent sans être reconstruites.
- Démarrage plus rapide : l'application est précompilée (ReadyToRun) dans le paquet.
- Sérialisation du coffre générée à la compilation, vérifiée octet pour octet identique à l'ancienne : prépare la compilation native.
- Icônes refaites à toutes les tailles demandées par Windows et le Store (barre des tâches, menu Démarrer, écran de démarrage), nettes de 16 à 256 pixels.
- **Microsoft Store** : `tools\store.ps1` produit le paquet à déposer dans l'Espace partenaires (identité du Store, sans l'autorisation de mise à jour automatique). Installé depuis le Store, Coffre ne vérifie plus ses mises à jour lui-même : « Rechercher une mise à jour » ouvre la page du Store. Fiche du Store prête dans docs/STORE.md, politique de confidentialité publiée sur le site (confidentialite.html).
- Pièce jointe sur n'importe quel élément (et plus seulement les documents) : menu ⋮ de la fiche › « Ajouter une pièce jointe… ».
- En-têtes de la liste et de la fiche alignés : « Toutes les catégories », le filtre et le tri sont à la même hauteur que le propriétaire et le coffre de l'élément ouvert.
- Code : réglages et barre latérale découpés en plusieurs fichiers, sans changement de comportement.

**Coffre pour macOS (première version)**
- Application Mac native (SwiftUI, macOS 13 ou plus récent, Apple Silicon et Intel), à télécharger en **Coffre-0.1.5-mac.dmg**.
- Ouvre le même fichier `.vault` que la version Windows, avec le même mot de passe maître (et la même clé secrète si tu en as une) : place-le dans iCloud Drive, OneDrive ou Dropbox. Les modifications faites sur le PC et sur le Mac sont fusionnées automatiquement, avec les mêmes règles que sur Windows.
- Écran de verrouillage identique dans l'esprit : ta photo de profil en carré arrondi, anneau animé pendant la vérification, Touch ID en bouton principal, jamais ton nom.
- Barre latérale (tous les éléments, favoris, catégories, coffres, tags, Sentinelle, corbeille), recherche, fiche avec copie au clic, code 2FA qui défile, création et modification des éléments avec le même générateur de mots de passe.
- Sentinelle : mots de passe faibles, réutilisés, comptes en double, score ; vérification facultative des mots de passe compromis (Have I Been Pwned, k-anonymat), comme sur Windows.
- Presse-papiers effacé automatiquement, secrets marqués confidentiels ; verrouillage automatique et à la mise en veille.
- Coffre sur Mac vérifie lui aussi les mises à jour sur le site.
- Pas encore sur Mac : remplissage dans le navigateur, passkeys, pièces jointes, coffres partagés, envois, Mode voyage, import et export. Ces données sont conservées intactes et restent utilisables depuis Windows.

## Installer

1. Télécharge `Coffre-0.1.5-kit.zip` depuis la [dernière version](https://github.com/sierrda-dev/coffre/releases/latest).
2. Clic droit › **Extraire tout**, puis double-clic sur **Installer Coffre**.
3. Windows demande d'approuver l'éditeur de Coffre une seule fois par ordinateur.

## Sécurité

Les paquets sont signés par le certificat [Coffre.cer](https://sierrda-dev.github.io/coffre/Coffre.cer) ; Windows refuse une mise à jour signée par un autre. Le site ne reçoit rien de ton coffre : l'application y lit seulement [version.json](https://sierrda-dev.github.io/coffre/version.json).

Ce dépôt contient le site de téléchargement et des mises à jour. Il est publié par `tools/release.ps1 -Publish`.
