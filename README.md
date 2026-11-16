# asukey

Gestionnaire de mots de passe **local** pour Windows 11 et macOS, chiffré de bout en bout, sans compte en ligne.

**Dernière version : 0.1.5.1** (16 novembre 2026)

- **Télécharger** : [https://sierrda-dev.github.io/coffre](https://sierrda-dev.github.io/coffre) (kit d'installation et version portable)
- **Déjà installé** (0.1.2 ou plus récent) : asukey propose les mises à jour tout seul.
- **Toutes les versions** : [Releases](https://github.com/sierrda-dev/coffre/releases) · [Journal des versions](CHANGELOG.md)

## Nouveautés de la 0.1.5.1

**Coffre s'appelle désormais asukey**
- Nouveau nom partout : fenêtre, menu Démarrer, barre des tâches, extension de navigateur, extension VS Code, application Mac et ligne de commande. La mise à jour s'installe par-dessus l'ancienne version comme d'habitude : ton coffre, tes réglages, Windows Hello, la clé secrète et l'extension déjà associée sont conservés.
- Rien ne bouge sur le disque : un coffre existant reste dans `Documents\Coffre`. Les nouvelles installations utilisent `Documents\asukey\asukey.vault`, et les nouvelles sauvegardes s'appellent `asukey-sauvegarde-…` (les anciennes restent listées et restaurables).
- Ligne de commande : la commande s'appelle `asukey` (`asukey run`, `asukey read`, `asukey mcp`…). L'installateur du kit installe aussi `coffre` pour que tes scripts continuent de marcher, et retire l'ancien dossier du PATH (si tu as configuré la signature Git, relance `asukey git setup`).
- Les références de secrets s'écrivent `asukey://Coffre/Élément/champ` ; les anciennes références `coffre://…` restent reconnues partout (ligne de commande, fichiers .env, modèles, extension VS Code).

**Apparence personnalisable**
- **Nouvelle icône** : disque bleu-violet avec trou de serrure, entouré d'un anneau, sur Windows (barre des tâches, menu Démarrer, Store), dans l'extension de navigateur et sur Mac. Aux petites tailles, seul le disque est gardé pour rester net.
- Nouvelle rubrique **Réglages › Apparence** : thème (comme Windows, clair, sombre), densité **Confortable** ou **Compact** (lignes de la liste et de la barre latérale plus serrées), taille de l'interface de 80 à 150 % (boutons − et +, ou Ctrl+= et Ctrl+−, Ctrl+0 pour revenir à 100 %), et « Rétablir les valeurs par défaut ». Tout s'applique immédiatement, sans redémarrer.
- **Barre latérale** : choisis les rubriques toujours affichées (Catégories, Tags) et, en option, le nombre d'éléments à côté de chaque rubrique.
- **Couleur de la barre latérale** : neuf teintes (Brume, Lavande, Menthe, Sable, Pétale, Ardoise, Nuit, Prune, Forêt) ou une couleur personnalisée ; le texte passe en clair ou en foncé selon la couleur.
- **Couleur d'accent** : bleu d'asukey ou huit autres couleurs, ou une couleur personnalisée, pour les boutons, la sélection et les liens.
- **Installer l'extension de navigateur depuis asukey** : menu ⋯ › « Installer l'extension de navigateur… » (ou Réglages › Navigateur). Choisis Chrome, Edge, Brave ou Firefox : asukey prépare l'extension (livrée avec l'application), copie le chemin, ouvre la page des extensions du navigateur, affiche les deux derniers clics et le code d'association dans la même fenêtre. L'extension installée est actualisée toute seule à chaque mise à jour d'asukey.
- **Enregistrement automatique des identifiants, plus fiable** : la bulle « Enregistrer dans asukey ? » apparaît aussi pour les connexions en deux pages (l'identifiant de la première page est repris), les sites sans vrai formulaire ou dont le bouton n'a pas de texte reconnaissable, les applications monopages (le champ du mot de passe disparaît après la connexion) et les connexions suivies d'une redirection. asukey verrouillé : la bulle propose « Déverrouiller et enregistrer » et enregistre dès le déverrouillage. Extension non associée ou asukey fermé : un message le dit au lieu de ne rien faire.
- **Nouvelle fenêtre de l'extension** : compte, recherche dans tout le coffre, générateur et bouton + en haut ; à gauche les suggestions pour le site ouvert (ou tous les identifiants, ou les favoris) ; à droite la fiche avec « Remplir automatiquement », le nom d'utilisateur et le mot de passe (masqué, robustesse affichée) copiés d'un clic, le code 2FA et les sites web. Navigation au clavier (flèches, Entrée pour remplir).
- **Deuxième appareil plus simple** : au premier lancement, « J'utilise déjà asukey sur un autre appareil » cherche les coffres dans OneDrive, Dropbox, Google Drive et iCloud et les ouvre en un clic (même mot de passe maître). **Réglages › Synchronisation** liste OneDrive, Dropbox, Google Drive et iCloud : « Synchroniser avec… » place le coffre dans le dossier « asukey » du service en un clic ; un service absent propose « Installer… » ; si un coffre y est déjà (venu d'un autre appareil), asukey propose de l'ouvrir au lieu de l'écraser. « Autre dossier » reste disponible pour Nextcloud, un NAS ou Syncthing.
- **Connexion directe à OneDrive, Google Drive et pCloud** (Réglages › Synchronisation › « Se connecter… ») : connexion au compte dans le navigateur, choix ou création du dossier dans le cloud, puis asukey envoie lui-même le coffre chiffré — à l'ouverture, toutes les minutes, après chaque modification et au verrouillage — et récupère la dernière version avant le déverrouillage. Deux appareils qui écrivent en même temps : fusion élément par élément, puis nouvel envoi. Pièces jointes copiées aussi. Sur un nouvel appareil : « J'utilise déjà asukey sur un autre appareil › Me connecter à… ». Chaque service doit d'abord être enregistré une fois (gratuit, docs/CLOUD.md). iCloud n'autorise pas la connexion directe : il passe par iCloud pour Windows.
- **Via l'application du service** : pCloud Drive rejoint OneDrive, Dropbox, Google Drive et iCloud, et « Choisir le dossier… » permet de choisir ou créer le sous-dossier dans chacun.
- **Quitter asukey** depuis le menu ⋯ de la barre latérale et le menu du compte (Ctrl+Q) : le coffre est verrouillé puis l'application se ferme.
- La rubrique **Développeur** est retirée de la barre latérale, des réglages et de la Sentinelle (les fonctions restent dans le code pour plus tard).
- Pièce jointe sur n'importe quel élément : menu ⋮ de la fiche › « Ajouter une pièce jointe… ».

## Installer

1. Télécharge `asukey-0.1.5.1-kit.zip` depuis la [dernière version](https://github.com/sierrda-dev/coffre/releases/latest).
2. Clic droit › **Extraire tout**, puis double-clic sur **Installer asukey**.
3. Windows demande d'approuver l'éditeur d'asukey une seule fois par ordinateur.

## Sécurité

Les paquets sont signés par le certificat [Coffre.cer](https://sierrda-dev.github.io/coffre/Coffre.cer) ; Windows refuse une mise à jour signée par un autre. Le site ne reçoit rien de ton coffre : l'application y lit seulement [version.json](https://sierrda-dev.github.io/coffre/version.json).

Ce dépôt contient le site de téléchargement et des mises à jour. Il est publié par `tools/release.ps1 -Publish`.
