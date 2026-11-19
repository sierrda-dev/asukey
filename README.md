# asukey

Gestionnaire de mots de passe **local** pour Windows 11, chiffré de bout en bout, sans compte en ligne.

**Dernière version : 0.1.5.2** (19 novembre 2026)

- **Télécharger** : [https://sierrda-dev.github.io/coffre](https://sierrda-dev.github.io/coffre) (kit d'installation et version portable)
- **Déjà installé** (0.1.2 ou plus récent) : asukey propose les mises à jour tout seul.
- **Toutes les versions** : [Releases](https://github.com/sierrda-dev/coffre/releases) · [Journal des versions](CHANGELOG.md)

## Nouveautés de la 0.1.5.2

**Partage : plus simple et plus convivial**
- **Nouvelle page Partage** (barre latérale) : une page d'accueil explique le partage en trois étapes ; ensuite, chaque coffre partagé y a sa carte avec les membres (pastilles, rôle, empreinte en info-bulle), les invitations en cours, l'état du fichier (« À jour · dernière modification il y a 5 min », « Fichier introuvable » avec « Retrouver le fichier… ») et des boutons Inviter, Ouvrir, Gérer. En bas, l'**activité récente** : « Marie a modifié « Netflix » · il y a 2 h ».
- **Assistant « Nouveau coffre partagé »** : un modèle (Famille, Couple, Équipe, Autre), un nom, puis l'endroit où le ranger parmi les services détectés (OneDrive, Google Drive, Dropbox, iCloud, pCloud — dans « asukey\Partagés ») ou un autre dossier, sans fenêtre « Enregistrer sous ». L'invitation suit directement.
- **Invitation en une étape** : tu indiques un prénom et ce que la personne pourra faire (ajouter et modifier, ou voir et copier). asukey dépose l'invitation dans le dossier partagé et te donne un **code de six mots** (« tigre · velours · nuage… »), avec un message prêt à envoyer (copier, ou e-mail). Plus besoin d'échanger des codes « COFFRE1-… » : l'ancienne méthode reste disponible dans « Gérer » › avancé.
- **« J'ai reçu une invitation »** : asukey trouve tout seul les invitations dans tes dossiers synchronisés ; tu tapes le code (majuscules, tirets et accents ignorés) et tu vois le coffre aussitôt, en lecture seule. La confirmation est automatique : dès que le propriétaire ouvre asukey, la personne devient membre (avec ses propres clés) et il reçoit « Marie a rejoint « Famille » ».
- **Identité en emojis** : chaque personne a une empreinte de six emojis (🐢 🍋 🚲 🌙 …) à comparer de vive voix, plus simple que l'empreinte hexadécimale (toujours visible en info-bulle).
- **Le fichier partagé se retrouve tout seul** sur chaque ordinateur : asukey retient son emplacement dans le service (« OneDrive › asukey › Partagés › Famille »), et le cherche aussi par son identifiant s'il a été renommé ou déplacé. Fini « Fichier partagé introuvable » sur un deuxième PC.
- **Partager un élément** : menu ⋯ de la fiche › « Partager avec… » : un coffre partagé existant, ou « Nouveau coffre partagé… » qui y place l'élément.
- **Partager un coffre existant** : clic droit sur le coffre › « Partager ce coffre… » (choix du service, puis invitation).
- Invitations limitées dans le temps (3 à 30 jours) et annulables ; annuler change la clé du coffre. La clé du coffre contenue dans une invitation est chiffrée avec une clé tirée du code par Argon2id (64 Mio) : sans le code, le fichier d'invitation ne sert à rien.

**Démarrage fiabilisé**
- Corrige asukey qui ne se lançait plus (sans aucun message) après avoir choisi une couleur d'accent dans Réglages › Apparence.
- Une erreur de thème ou de couleur au lancement est ignorée et notée dans le journal, au lieu d'empêcher l'ouverture.
- Mode sans échec : si asukey n'arrive pas à démarrer deux fois de suite, l'apparence est remise par défaut au lancement suivant, avec un message pour l'expliquer.
- Les réglages d'apparence invalides (fichier modifié à la main, par exemple) reviennent aux valeurs par défaut.
- Publication : chaque version est d'abord lancée automatiquement avec plusieurs réglages d'apparence (dont les tiens) ; si elle ne démarre pas, rien n'est publié.

## Installer

1. Télécharge `asukey-0.1.5.2-kit.zip` depuis la [dernière version](https://github.com/sierrda-dev/coffre/releases/latest).
2. Clic droit › **Extraire tout**, puis double-clic sur **Installer asukey**.
3. Windows demande d'approuver l'éditeur d'asukey une seule fois par ordinateur.

## Sécurité

Les paquets sont signés par le certificat [Coffre.cer](https://sierrda-dev.github.io/coffre/Coffre.cer) ; Windows refuse une mise à jour signée par un autre. Le site ne reçoit rien de ton coffre : l'application y lit seulement [version.json](https://sierrda-dev.github.io/coffre/version.json).

Ce dépôt contient le site de téléchargement et des mises à jour. Il est publié par `tools/release.ps1 -Publish`.
