# asukey

Gestionnaire de mots de passe **local** pour Windows 11, chiffré de bout en bout, sans compte en ligne.

**Dernière version : 0.1.9** (25 novembre 2026)

- **Installer** : [Microsoft Store](https://apps.microsoft.com/detail/9PNJ014KZP63) (conseillé : mises à jour automatiques)
- **Télécharger** : [https://sierrda-dev.github.io/asukey](https://sierrda-dev.github.io/asukey) (kit d'installation)
- **Déjà installé** (0.1.2 ou plus récent) : asukey propose les mises à jour tout seul.
- **Toutes les versions** : [Releases](https://github.com/sierrda-dev/asukey/releases) · [Journal des versions](CHANGELOG.md)

## Nouveautés de la 0.1.9

**Projets renommés** (code source uniquement) : `asukey.sln`, `Asukey.App`, `Asukey.Core`, `Asukey.Cli`, `Asukey.Tests`, espaces de noms `Asukey.*`. L'application s'appelle désormais **asukey.exe** (Gestionnaire des tâches). Les données gardent leurs emplacements (`%LOCALAPPDATA%\Coffre`, clé Windows Hello, stratégie d'entreprise) : rien ne change pour les utilisateurs.

**Publication GitHub** : le Microsoft Store est proposé en premier (site, README du dépôt, notes de version) dès que son identifiant est dans `packaging/microsoft-store.txt` ; la ligne de commande `asukey.exe` est jointe à chaque version (`asukey-<version>-ligne-de-commande.zip`), à côté du kit.

**Design Windows 11 (Fluent 2)**
- Couleurs de Fluent : texte principal et secondaire, couleurs d'état (succès, attention, erreur) de WinUI.
- **Contraste élevé** de Windows respecté : couleurs du thème de contraste choisi, sans transparence.
- Échelle typographique de Fluent partout (12 légende, 14 corps, 18, 20 sous-titre, 28 titre) et police Segoe UI Variable.
- **Menu du clic droit dans la liste comme l'Explorateur de Windows 11** : actions rapides en icônes en haut (copier l'identifiant, le mot de passe, le code 2FA, favori, corbeille), le reste en liste dessous.
- **Recherche avec suggestions**, comme dans Paramètres de Windows 11 : sous le champ du haut, les fiches récentes (champ vide) ou les éléments qui correspondent, les rubriques des réglages et « Créer un identifiant « … » ». Flèches pour choisir, Entrée pour ouvrir, Échap pour fermer ; la liste de gauche continue de se filtrer.
- **Plus de blocages** : copie de référence et presse-papiers occupé, logos de sites lents ou sans adresse (15 s au plus par site, IPv6/IPv4 en alternance).
- Animations de Windows 11 : la fiche glisse doucement à l'ouverture d'un élément, et les cartes des Réglages arrivent l'une après l'autre (coupées si Windows désactive les animations).
- **Réglages comme l'application Paramètres de Windows 11** : une carte par réglage (espacées de 4 px), titres de groupe en semi-gras, titre de page en 28 px, navigation à icônes colorées avec la barre d'accent sur la rubrique ouverte.

**Productivité**
- **Sélection multiple et actions groupées** : Ctrl+clic, Maj+clic ou Ctrl+A dans la liste, puis favoris, tag, déplacement vers un coffre, archives ou corbeille en une fois (restauration et suppression définitive dans la corbeille). Annulable comme une action simple ; les éléments en lecture seule d'un coffre partagé ne sont pas touchés.
- **Création assistée** : recherche des services sans tenir compte des accents ni des espaces (« credit agri »), catalogue élargi à plus de 180 services, logo du site dans les résultats ; une adresse tapée (« exemple.fr ») crée directement la connexion avec son titre. Dans l'éditeur, le titre se remplit d'après l'adresse, et un identifiant oublié est signalé avant l'enregistrement.
- Extension : plus aucun `innerHTML` (fenêtres, icônes) ; l'outil de vérification de Mozilla ne signale plus aucun avertissement.
- **Extension : asukey seul gestionnaire du navigateur** : un bandeau propose de couper l'enregistrement des mots de passe intégré à Chrome, Edge ou Firefox (et le remplissage des cartes et adresses dans Chrome et Edge), pour ne plus avoir deux propositions à chaque connexion. Autorisation facultative « privacy », demandée seulement à ce moment.

**Synchronisation directe**
- **OneDrive en connexion directe** : Réglages › Synchronisation › OneDrive › « Se connecter… » ; rien à installer, asukey envoie lui-même ton coffre chiffré (comptes Microsoft personnels et professionnels).
- Connexion au compte corrigée : elle pouvait rester bloquée après l'autorisation dans le navigateur (le navigateur ouvre des connexions à l'avance sans rien y envoyer ; asukey attendait sur l'une d'elles).
- Connexion aux services en IPv6 et IPv4 en parallèle : quand l'IPv6 de la box ou de l'opérateur ne mène nulle part, asukey passe aussitôt par l'IPv4 (l'échange du code avec Microsoft dépassait son délai).
- Toute erreur de connexion s'affiche, et chaque étape est notée dans le journal.
- Fenêtre « Synchroniser avec… » : le texte revient à la ligne au lieu d'être coupé.
- Bouton « Se déconnecter de … » directement dans le bandeau et sur la ligne du service (avant : caché dans le menu ⋯) ; « Arrêter la synchronisation… » remet le coffre sur ce PC quand il passe par l'application d'un service.
- Page Synchronisation revue : bandeau d'état (service, compte, dernière synchronisation), puis OneDrive et Google Drive. Dropbox, iCloud Drive et pCloud reviendront avec leur connexion directe (un service déjà utilisé reste affiché). Logo officiel du service si son fichier est déposé dans `Assets\Services`.

## Installer

1. Télécharge `asukey-0.1.9-kit.zip` depuis la [dernière version](https://github.com/sierrda-dev/asukey/releases/latest).
2. Clic droit › **Extraire tout**, puis double-clic sur **Installer asukey**.
3. Windows demande d'approuver l'éditeur d'asukey une seule fois par ordinateur.

**Ligne de commande** (développeurs) : `asukey-0.1.9-ligne-de-commande.zip` dans la [dernière version](https://github.com/sierrda-dev/asukey/releases/latest), puis double-clic sur **Installer la ligne de commande**.

## Sécurité

Les paquets sont signés par le certificat [Coffre.cer](https://sierrda-dev.github.io/asukey/Coffre.cer) ; Windows refuse une mise à jour signée par un autre. Le site ne reçoit rien de ton coffre : l'application y lit seulement [version.json](https://sierrda-dev.github.io/asukey/version.json).

Ce dépôt contient le site de téléchargement et des mises à jour. Il est publié par `tools/release.ps1 -Publish`.
