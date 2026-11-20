# Journal des versions

## 0.1.6.1 — 20 novembre 2026

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

## 0.1.6 — 19 novembre 2026

**Nouveau look Windows 11 (Fluent)**
- **Fenêtre transparente** : la barre latérale et la barre du haut forment un seul bloc translucide (Acrylique : le bureau se voit, flouté, derrière la fenêtre) ; la liste et la fiche sont posées sur une couche claire au coin arrondi. Réglages › Apparence › **Transparence** : Acrylique, Mica (teinte du fond d'écran) ou Aucune (fonds unis comme avant). Le mode sans échec coupe la transparence. Une couleur de barre latérale choisie devient une teinte translucide.
- **Barre latérale de Windows 11** : rubriques à icônes simples, barre de la couleur d'accent sur la rubrique active, sections « Coffres », « Catégories », « Tags » en petit titre, catégories en petites tuiles colorées. Le **profil passe en bas** (« Profil et réglages », état de la synchronisation, roue dentée pour les réglages ; clic droit : nouveau coffre, partage, verrouiller, quitter).
- **Recherche** centrée dans la barre du haut, dans un encadré bien visible, loupe à gauche et raccourci « Ctrl+F » à droite. Raccourcis dans les info-bulles (Nouvel élément : Ctrl+N, Aide : F1, nouveau) et dans les menus (Verrouiller : Ctrl+L, Quitter : Ctrl+Q).
- **Arrondis de Windows 11** : 4 px pour les boutons, champs et listes, 8 px pour les cartes, bandeaux et fenêtres.
- **Boutons de Windows 11** : bouton d'accent plein pour l'action principale (Nouvel élément, Modifier, Enregistrer…), boutons clairs à fin relief pour les autres. Le bleu d'asukey est aussi utilisé par les interrupteurs, cases et contours de focus quand aucune couleur d'accent n'est choisie.
- **Sélection** : l'élément sélectionné dans la liste a un fond discret et une petite barre de la couleur d'accent (au lieu d'un fond bleu plein).
- **Écran de verrouillage** : logo d'asukey, Windows Hello et mot de passe dans une carte claire posée sur le fond translucide.
- **Logos des sites** : les identifiants affichent le logo de leur site, téléchargé directement depuis le site lui-même (aucun service tiers, aucune donnée du coffre envoyée), puis gardé sur l'ordinateur. Sans logo, une tuile de couleur avec l'initiale. Désactivable dans Réglages › Apparence › Logos des sites ; jamais pour les adresses locales (localhost, adresses IP, NAS…).
- Fiche : titres plus grands, libellés des champs en gris discret. Liste plus aérée (lignes plus hautes, textes plus grands) ; les logos des sites occupent toute la tuile.
- Prépare la publication sur le Microsoft Store (numéro de version à trois chiffres).
- **Comptes** : en bas de la barre latérale, ta photo et ton nom ouvrent le menu du compte (gérer le compte, gérer les comptes, configurer un autre appareil, nouveau coffre, réglages, verrouiller, quitter).
  - « **Comptes** » liste les coffres déjà ouverts sur cet ordinateur : passe de l'un à l'autre (asukey se verrouille et demande le mot de passe de l'autre coffre), ajoute un compte (coffre existant ou nouveau), retire un compte de la liste.
  - « **Gérer le compte** » : photo, prénom, nom, **adresse e-mail** (nouveau) et téléphone ; connexion et récupération (mot de passe maître, Windows Hello, clé secrète, kit d'urgence) ; appareils et synchronisation. La rubrique « Profil » des réglages disparaît.
  - « **Configurer un autre appareil** » : les étapes pour ouvrir le même coffre sur un autre ordinateur ou sur iPhone, selon ta synchronisation.
  - Raccourci **Ctrl+,** pour ouvrir les réglages.
- **Nouvel écran Réglages › À propos** : bandeau illustré aux couleurs d'asukey, logo et version, mode d'installation (kit, Microsoft Store), date de la dernière vérification avec « Rechercher une mise à jour » et « Nouveautés de cette version », vérification quotidienne, puis conditions d'utilisation, politique de confidentialité, journal des versions et guide.
- Un coffre dont le contenu déchiffré n'est pas du texte valide est refusé à l'ouverture (au lieu de s'ouvrir puis d'échouer à l'enregistrement).
- Corrige l'erreur « Aucun composant installé n'a été détecté » après « Vérifier les fuites maintenant » (ou après avoir ignoré une alerte) dans la Sentinelle.
- La version portable (sans installation) n'est plus publiée : une version GitHub contient le kit d'installation et le paquet de mise à jour.

## 0.1.5.2 — 19 novembre 2026

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

## 0.1.5.1 — 16 novembre 2026

**Coffre s'appelle désormais asukey**
- Nouveau nom partout : fenêtre, menu Démarrer, barre des tâches, extension de navigateur, extension VS Code et ligne de commande. La mise à jour s'installe par-dessus l'ancienne version comme d'habitude : ton coffre, tes réglages, Windows Hello, la clé secrète et l'extension déjà associée sont conservés.
- Rien ne bouge sur le disque : un coffre existant reste dans `Documents\Coffre`. Les nouvelles installations utilisent `Documents\asukey\asukey.vault`, et les nouvelles sauvegardes s'appellent `asukey-sauvegarde-…` (les anciennes restent listées et restaurables).
- Ligne de commande : la commande s'appelle `asukey` (`asukey run`, `asukey read`, `asukey mcp`…). L'installateur du kit installe aussi `coffre` pour que tes scripts continuent de marcher, et retire l'ancien dossier du PATH (si tu as configuré la signature Git, relance `asukey git setup`).
- Les références de secrets s'écrivent `asukey://Coffre/Élément/champ` ; les anciennes références `coffre://…` restent reconnues partout (ligne de commande, fichiers .env, modèles, extension VS Code).

**Apparence personnalisable**
- **Nouvelle icône** : disque bleu-violet avec trou de serrure, entouré d'un anneau, sur Windows (barre des tâches, menu Démarrer, Store) et dans l'extension de navigateur. Aux petites tailles, seul le disque est gardé pour rester net.
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

## 0.1.5 — 16 novembre 2026

**Sécurité des données**
- **Mises à jour signées** : l'annonce de chaque version (version.json) est signée avec une clé gardée sur le PC de publication, et contient l'empreinte de chaque fichier publié. Coffre refuse toute mise à jour dont la signature ne correspond pas : un compte GitHub piraté ne suffirait plus à diffuser un faux Coffre.
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
- En-têtes de la liste et de la fiche alignés : « Toutes les catégories », le filtre et le tri sont à la même hauteur que le propriétaire et le coffre de l'élément ouvert.
- Code : réglages et barre latérale découpés en plusieurs fichiers, sans changement de comportement.

## 0.1.4 — 13 novembre 2026

**Plus rapide, nouvel écran de verrouillage, éditeur et réglages revus**
- La liste des éléments ne crée plus que les lignes visibles (une vingtaine), recyclées en défilant, au lieu d'une ligne par élément : ouverture, défilement et changement de coffre ou de filtre restent fluides même avec des milliers d'éléments. Apparence, regroupements, clic droit et flèches du clavier inchangés.
- La recherche attend 150 ms après la dernière frappe au lieu de tout recalculer à chaque lettre, et cherche dans un texte préparé une fois par élément (titre, identifiant, e-mail, site, tags, notes).
- L'analyse de la Sentinelle se fait en arrière-plan : plus de petit gel après chaque enregistrement sur un gros coffre. Les pastilles, le compteur de la barre latérale et la fiche ouverte se mettent à jour d'eux-mêmes.
- Mesures de performance dans le journal local de Coffre (%LOCALAPPDATA%\Coffre\coffre.log) : temps de démarrage, temps d'ouverture du coffre et mémoire utilisée. Rien n'est envoyé.
- **Nouvel écran de verrouillage**, épuré et sans encadré : ta photo de profil au centre (ou le logo de Coffre), Windows Hello en bouton principal quand il est disponible, puis le mot de passe ; avertissement « Verr. Maj est activée », secousse du champ en cas d'erreur, rappel du verrouillage automatique et de Ctrl+Q en bas. Ton nom n'apparaît jamais. La photo est copiée hors du coffre pour s'afficher avant le déverrouillage : Réglages › Sécurité › « Photo sur l'écran de verrouillage » pour la retirer.
- **Animation de déverrouillage** autour de la photo de profil : un anneau en dégradé tourne pendant la vérification ; au déverrouillage, la photo rebondit légèrement et l'anneau s'élargit en s'effaçant (« Coffre déverrouillé ») ; en cas d'erreur, il rougit un instant. Rien ne bouge si les effets d'animation sont désactivés dans Windows.
- **Formes harmonisées** : une seule échelle d'arrondis dans toute l'application (petits boutons 6, boutons et champs 8, cartes et bulles 12). Photos de profil, initiales, icônes de coffre et pastilles d'icônes ont la même forme de carré arrondi que les tuiles des éléments, y compris sur l'écran de verrouillage. Marges de la barre latérale alignées (photo du compte et rubriques au même retrait).
- **Watchtower devient la Sentinelle** (barre latérale, page, journal, aide). En ligne de commande : `coffre sentinelle` (`coffre watchtower` reste accepté).
- **Comportement du remplissage par site web** : le bouton à côté de chaque adresse propose « Remplir n'importe où sur ce site web » (par défaut : toutes les adresses du même site, par exemple login.exemple.fr et www.exemple.fr), « Remplir uniquement sur cet hôte précis » ou « Ne jamais remplir sur ce site web », avec une phrase qui dit où l'élément sera proposé.
- **Mot de passe dans l'éditeur** : au clic, il s'affiche en clair et une bulle propose « Créer un nouveau mot de passe ». Le générateur s'ouvre sous le champ : Annuler, ↻, Utiliser ; aperçu avec chiffres en bleu et symboles en rouge, barre de robustesse ; type (aléatoire, mémorisable, code PIN), nombre de caractères, chiffres, symboles. Les choix sont mémorisés.
- **Réglages** : colonne de gauche avec une tuile de couleur par rubrique, rubrique ouverte en bleu.
- **Illustration** de la fiche vide redessinée, plus abstraite : anneaux, formes arrondies et points aux couleurs de Coffre.
- Nouveau test automatique sur un coffre de 5 000 éléments (enregistrement, modification, Sentinelle, réouverture), pour repérer toute version qui ralentirait.

## 0.1.3 — 13 novembre 2026

**Nouveautés visibles et publication**
- Après une mise à jour, Coffre affiche « Coffre a été mis à jour » avec les nouveautés de la version installée, et un lien vers le journal complet.
- Réglages › À propos › **Voir le journal des versions** ouvre l'historique sur GitHub.
- Chaque version publiée sur GitHub contient les nouveautés complètes, la marche à suivre pour installer ou mettre à jour, et l'empreinte SHA-256 de chaque fichier.
- La page d'accueil du dépôt GitHub présente la dernière version et ses nouveautés ; le journal complet y est publié (CHANGELOG.md).
- Le numéro de version ne se change plus qu'à un endroit (Directory.Build.props) : l'application, la ligne de commande et le paquet s'alignent dessus.
- Correction : le menu « Copier la référence » d'un élément Environnement propose bien la commande « coffre run » (la 0.1.1 l'avait placée dans « Afficher en grand », ce qui empêchait la compilation).

## 0.1.2 — 13 novembre 2026

**Mises à jour automatiques**
- Coffre vérifie chaque jour s'il existe une nouvelle version et propose de l'installer, avec la liste des nouveautés.
- « Mettre à jour maintenant » : Coffre se verrouille, Windows télécharge et installe la version signée, puis relance Coffre ; coffre et réglages conservés.
- « Plus tard » repousse la proposition de trois jours ; Réglages › À propos › Mises à jour automatiques pour désactiver.
- Version portable : la fenêtre ouvre la page de téléchargement.
- Site des mises à jour : https://sierrda-dev.github.io/coffre ; tools/release.ps1 -Publish publie la version GitHub et le site en une commande.

## 0.1.1 — 13 novembre 2026

**Plusieurs ordinateurs, accès d'urgence et développeurs**
- **Synchronisation entre tes ordinateurs, sans serveur** : le coffre se place dans un dossier OneDrive, Dropbox, Google Drive ou NAS (Réglages › Synchronisation › Déplacer le coffre).
  - Coffre surveille le fichier toutes les 5 secondes et avant chaque enregistrement, puis fusionne élément par élément : la modification la plus récente gagne.
  - Les suppressions définitives laissent une trace (180 jours) pour qu'un élément effacé ne revienne pas depuis l'autre ordinateur.
  - Les copies en conflit créées par OneDrive ou Dropbox (« Coffre-PC-BUREAU.vault ») sont fusionnées, puis renommées en `.fusionne-…`.
  - Un mot de passe maître changé sur un ordinateur est adopté par les autres au lieu d'être écrasé.
  - Le Mode voyage n'est jamais fusionné.
- **Accès d'urgence** par un contact de confiance (Réglages › Accès d'urgence) :
  - fichier `.coffre-secours` chiffré pour la clé X25519 du contact (son code de partage), avec une copie chiffrée du coffre ;
  - le contact l'ouvre depuis son propre Coffre, obtient une copie et choisit un nouveau mot de passe ; ni le propriétaire ni son kit d'urgence ne sont touchés.
- **Environnements** : nouvelle catégorie (une variable par champ), import d'un `.env` dans l'éditeur, `coffre run --environment Coffre/Élément`, `coffre env import` et `coffre env export`. Les valeurs sensibles sont masquées dans la sortie. La référence `coffre://coffre/élément/*` renvoie toutes les variables.
- **Serveur MCP** `coffre mcp` pour les assistants d'IA (Claude, VS Code, Cursor) :
  - `list_items` donne les titres, sites, identifiants et références `coffre://`, jamais les secrets (accord une fois par déverrouillage) ;
  - `read_secret` demande ton accord dans Coffre **à chaque lecture**, sans l'option des 10 minutes.
  - Réglages › Développeur › Copier la configuration.
- **Extension VS Code** (dans le kit, installée sans Marketplace) : insérer une référence (Ctrl+Alt+K), secrets en clair soulignés avec correction rapide, analyse du dossier, lancement avec un environnement, explication au survol des références.

## 0.1.0 — 13 novembre 2026

**Première version d'utilisation**
- **Sentinelle redessinée** :
  - **En-tête** : titre, explication, bouton **Partager mon score** (copie un résumé sans aucune information sur tes éléments), et cadran du score à droite (arc dégradé, graduations, appréciation « FANTASTIQUE », « TRÈS BON »…).
  - **Robustesse globale des mots de passe** : barre en cinq couleurs, de « Fantastique » à « Très faible », avec légende.
  - **Grandes tuiles** sur trois colonnes, seulement pour les problèmes réels : nombre, titre, explication, icône pâle, et « Afficher les éléments → ». Nouvelles tuiles : **Clé de récupération manquante** (→ Configurer) et **Éléments avec doublons** (même site et même identifiant).
  - **Alertes ignorées** : « Ignorer » sur chaque élément signalé, puis « Afficher les alertes ignorées » pour les rétablir. Ignorer ne modifie ni la date ni l'historique de l'élément.
- Toutes les corrections de la série 0.0.9 : invitations, page Profil, ligne de commande en un seul fichier.

## 0.0.9 — 13 novembre 2026

**Développeurs et confort**
- **Références de secrets** `coffre://coffre/élément/champ` :
  - champs désignés par leur clé, un alias (« mot de passe », « token »), un libellé de champ personnalisé, ou « otp » pour le code 2FA actuel ;
  - clic droit sur un élément › **Copier la référence**.
- **Ligne de commande** :
  - `coffre read`, `coffre run --env-file .env -- commande` (secrets masqués dans la sortie, `--no-masking` pour les programmes interactifs) et `coffre inject` (modèles `{{ coffre://… }}`) ;
  - ces commandes demandent les secrets à **Coffre ouvert**, qui affiche une autorisation (option « Ne plus demander pendant 10 minutes »). Sans l'application ouverte, la ligne de commande demande le mot de passe maître ;
  - le kit contient `coffre.exe` et « Installer la ligne de commande ».
- **Plugins** : `coffre plugin init gh coffre://Personnel/GitHub`, puis `coffre gh …` injecte GH_TOKEN, sans fichier de configuration en clair. 14 outils sont pris en charge : gh, glab, aws, az, npm, docker, openai, claude, stripe, hf, vercel, netlify, doctl, terraform.
- **Signature des commits Git** avec une clé SSH du coffre, via l'agent de Coffre (accord demandé à chaque signature). Elle se configure par `coffre git setup` ou par Réglages › Développeur › Configurer Git. Vérifié : `git verify-commit` et `ssh-keygen -Y verify` acceptent les signatures Ed25519, ECDSA et RSA.
- **Sentinelle développeur** :
  - repère les clés SSH privées sans phrase de passe dans ~/.ssh ;
  - analyse un dossier de code à la recherche de secrets en clair : jetons GitHub, clés AWS, Stripe, OpenAI, Anthropic, Slack, Google, npm, clés privées, mots de passe dans les .env (valeurs masquées) ;
  - aussi disponible par `coffre scan <dossier>`.
- **Extension Firefox** (Firefox 128 et plus), dans le kit.
- **Afficher en grand** : caractères géants numérotés (chiffres en bleu, symboles en rouge) dans une fenêtre épinglable au-dessus des autres, fermée au verrouillage.
- **Clic droit dans la liste** : ouvrir, copier l'identifiant, le mot de passe ou le code 2FA, ouvrir le site, afficher en grand, copier la référence, favori, modifier, corbeille.
- **Saisie automatique** depuis l'accès rapide (**Ctrl+Maj+Entrée**) : Coffre revient à l'application précédente et y tape l'identifiant, Tab, puis le mot de passe, sans passer par le presse-papiers.
- **Page Profil** séparée des réglages :
  - photo et nom, avec le bouton « Gérer le profil » ;
  - carte **Identité** (adresse, téléphone, e-mail ; « Mettre à jour l'identité », « Changer ») ;
  - carte **Moyen de paiement** (« Sélectionner » la carte par défaut). L'extension propose cette identité et cette carte en premier.
  - La barre latérale affiche ta photo et ton nom en haut, et les coffres sous « COFFRES ».
- **Invitations corrigées** : le code de partage n'est plus effacé du presse-papiers après 30 secondes, ce qui pouvait faire échouer une invitation avec « CODE ».
  - Nouvelle fenêtre **Mon code de partage…** : copier, envoyer par e-mail ou enregistrer dans un fichier.
  - Le code collé dans « Inviter » est vérifié aussitôt et affiche le nom et l'empreinte de la personne.
  - Les erreurs de partage ont toutes un message clair.
- **Reporté après la 0.1.0** : déverrouillage par clé FIDO2 (YubiKey). Il passe par l'API WebAuthn native de Windows, avec des structures binaires qu'on ne peut pas valider sans clé physique ; une erreur ferait planter l'application.

## 0.0.8 — 13 novembre 2026

**Diffuser et utiliser à plusieurs**
- **Kit d'installation** fabriqué par `tools\release.ps1` sur le PC de l'éditeur. Il contient :
  - `Installer Coffre.cmd`, qui approuve le certificat de l'éditeur (une seule autorisation Windows par ordinateur) puis installe ou met à jour le paquet MSIX signé ;
  - une version portable de secours ;
  - l'extension Chrome/Edge ;
  - une notice LISEZ-MOI et le guide de démarrage.
- **Signature** : certificat auto-signé `CN=Erc` créé une fois dans le magasin de l'éditeur et réutilisé pour chaque version, afin que les mises à jour s'installent par-dessus. Les paquets sont horodatés quand Internet est disponible.
- **Mises à jour** : refaire « Installer Coffre » avec le nouveau kit. Le coffre (Documents\Coffre) et les réglages sont conservés. « Rechercher une mise à jour » l'explique, au lieu d'afficher une erreur.
- **Guide de démarrage** dans l'application (bouton « Aide », menu ⋮, écran de verrouillage, Réglages › À propos) : installation, mot de passe maître et kit d'urgence, import, extension, coffres partagés à plusieurs.
- **« Copier mon code de partage »** dans le menu ⋮, pour rejoindre un coffre partagé.
- La feuille de route « Développeurs et confort » (FIDO2, signature Git, `coffre run`…) passe en 0.0.9.

## 0.0.7.1 — 12 novembre 2026

**Interface repensée**
- **Barre latérale claire**, gris très léger, à la place du bleu nuit. On y trouve :
  - « Coffre ⋮ » en haut ;
  - le sélecteur « Tous les coffres » suivi d'un séparateur ;
  - Profil, Tous les éléments, Favoris, Sentinelle et Développeur (clés SSH et clés d'API) ;
  - les coffres sous le nom du propriétaire, avec + pour en créer un ;
  - les tags avec une icône verte.
- **Barre d'outils** : ← →, champ « Rechercher dans tous les coffres » avec loupe, lien bleu « Aide » et bouton bleu « + Nouvel élément ».
- **Liste** : groupes par mois (« NOVEMBRE 2026 »), triés par date de modification. Les tuiles affichent deux lettres sur fond pastel (« me », « Ed »), et la sélection est bleue avec du texte blanc.
- **Fiche** : boutons « Partager » (envoi sécurisé) et « Modifier ». Les libellés violets sont plus petits et les champs plus compacts. Le pied « › Dernière modification lundi 9 novembre 2026 à 20:11:03 » se déplie.
- **Sans sélection** : une illustration de coffre-fort en gris clair.
- **« Que souhaitez-vous ajouter ? »** :
  - recherche (catégories et services connus, par exemple « netflix ») ;
  - six cartes : Connexion, Note sécurisée, Carte de crédit, Identité, Identifiants de l'API, Document ;
  - « Plus de catégories » ;
  - « Importer vos données dans Coffre ».
- **Nouvel éditeur** :
  - ← et ✕ en haut ; grande icône avec ▾ pour changer de catégorie, puis le titre ;
  - carte de champs sans cadre, avec l'e-mail le plus utilisé proposé comme nom d'utilisateur ;
  - sites web sur fond gris, avec « + ajouter un autre site web » et ⊖ pour retirer ;
  - « + ajouter plus », pour l'e-mail, la 2FA et les champs personnalisés ;
  - remarques, puis tags en pastilles avec « + Ajouter un tag » ;
  - pied « propriétaire | coffre ▾ » et bouton « Enregistrer » (Ctrl+S).
- **Nouvel écran de verrouillage** :
  - la barre latérale grise reste visible, vide, avec « Coffre ⋮ » ;
  - au centre : le logo de Coffre, le champ « Entrez votre mot de passe » avec sa flèche bleue, et une ligne d'aide pour Windows Hello ;
  - le menu ⋮ propose : ouvrir un autre coffre, créer un coffre, mot de passe oublié, mises à jour, aide, fermer (Ctrl+W) et quitter (Ctrl+Q). Les actions qui demandent un coffre ouvert y sont grisées.
- **Confidentialité** : l'écran de verrouillage n'affiche plus de prénom, de photo, de nom de compte Windows ni de nom de fichier du coffre.

## 0.0.7 — 12 novembre 2026

**Partager et protéger**
- **Clé secrète** : clé aléatoire de 128 bits combinée au mot de passe maître (HKDF-SHA256). Une copie volée du fichier ne peut plus être attaquée par force brute. Elle est mémorisée sur l'appareil (DPAPI, compte Windows) et demandée une seule fois sur un nouvel ordinateur. Elle figure dans le kit d'urgence et se règle dans Réglages › Sécurité.
- **Mode voyage** : les coffres non marqués « sûrs pour le voyage » sont retirés de l'ordinateur et placés dans une archive chiffrée (`.coffre-voyage`) à ranger ailleurs, puis réintégrés au retour.
  - L'archive est vérifiée avant toute suppression.
  - Les sauvegardes automatiques sont suspendues pendant le voyage, et les sauvegardes locales existantes peuvent être supprimées.
  - Un bandeau s'affiche dans la barre latérale pendant le voyage.
- **Envoi sécurisé nominatif** : destinataires nommés, chacun avec son propre code ; durée de 1 heure à 30 jours. Un historique des envois (sans leur contenu) est conservé.
- **Qui a accès** dans chaque fiche : membres du coffre partagé et leurs rôles, plus les envois sécurisés. La fiche affiche aussi l'**historique des modifications** (date, auteur, appareil) avec restauration.
- **Échéances** :
  - Cartes, pièces d'identité (nouveau champ « Expiration de la pièce »), documents et clés d'API sont suivis. Les formats AAAA-MM-JJ et JJ/MM/AAAA sont acceptés.
  - Une rubrique « Expire bientôt » apparaît dans la barre latérale.
  - Une notification Windows est affichée au déverrouillage, au plus une fois par jour, et peut être désactivée.
- **Annuler** : un bouton « Annuler » apparaît pendant 6 secondes après un déplacement entre coffres ou une mise à la corbeille.
- **Aperçu des pièces jointes** : images et fichiers texte s'ouvrent dans Coffre, sans copie en clair sur le disque.

**Ligne de commande** : `coffre secret-key on|off`, `coffre travel status|on|off|safe`, `coffre send --to "Marie,Paul" --hours 1`. La clé secrète se fournit par `COFFRE_SECRET_KEY` ou est demandée à l'ouverture.

**Reporté à la 0.0.8** : déverrouillage par clé de sécurité FIDO2 (YubiKey, Titan). Il demande un module natif (API WebAuthn de Windows, extension hmac-secret) qui doit être testé sur du matériel réel.

**Limites assumées (sans serveur)** :
- Une page d'envoi déjà transmise ne peut pas être révoquée à distance. Son expiration est vérifiée par la page elle-même.
- Un coffre protégé par une clé secrète ne s'ouvre plus avec Coffre 0.0.6 ou antérieur.

**Tests** : 43 tests unitaires, dont 7 nouveaux (clé secrète, Mode voyage et archive modifiée, envoi nominatif, échéances, kit d'urgence) ; tests de bout en bout inchangés et réussis.

## 0.0.6 — 12 novembre 2026

**Remplir plus vite** : accès rapide (Ctrl+Maj+Espace) ; remplissage des cartes bancaires et des identités dans Chrome et Edge ; identifiant sur deux pages ; générateur de noms d'utilisateur (mots, aléatoire, alias « +site ») ; questions de sécurité avec réponse générée ; catalogue de 90 services à la création d'un élément ; brouillons chiffrés conservés au verrouillage ; Sentinelle « Passkeys disponibles ».
**Ligne de commande** : `coffre add` et `coffre generate --username`.
**Tests** : 36 tests unitaires ; nouveau test de bout en bout `tests/e2e/forms.e2e.js` (cartes, identités, nom d'utilisateur, deux pages).

## 0.0.5 — 12 novembre 2026

**Interface** : nouvelle disposition : barre latérale bleu nuit (compte, Tous les éléments, Favoris, Sentinelle, coffres et tags repliables, Archives, Supprimés récemment) ; barre d'outils en haut (précédent/suivant, recherche, aide, « Nouvel élément ») ; liste avec filtre « Toutes les catégories », tri, groupes par lettre, étoile des favoris et sélection bleue ; fiche avec propriétaire et coffre (déplacement vers un autre coffre), grande icône, champs en carte aux libellés bleu-violet, robustesse à droite du mot de passe, code à usage unique « 553 • 740 » avec compte à rebours, adresses web et détails sous la carte.
**Corrections** : compilation WinUI 3 (ScrollViewer scellé, conflits de noms), profil de lancement MSIX (`launchSettings.json`), déploiement activé dans la solution (x64 et ARM64), plantage au démarrage lié à la couleur d'accent, message d'erreur explicite si l'application ne peut pas démarrer.

## 0.0.4 — 9 novembre 2026

Première version native Windows 11 (WinUI 3, .NET 10, MSIX), qui remplace l'application Electron 2.x (ses coffres sont relus et convertis).

**Indispensables** : remplissage automatique Chrome/Edge (icône dans les champs, enregistrement et mise à jour proposés, générateur, codes 2FA) ; kit d'urgence PDF et clé de récupération ; sauvegardes automatiques chiffrées et vérifiées ; tests automatisés Windows et Linux en CI.
**Distribution** : paquet MSIX x64/ARM64, mises à jour automatiques par .appinstaller, signature en CI, extension prête pour le Chrome Web Store et Edge Add-ons, version portable.
**Fonctions avancées** : pièces jointes chiffrées ; historique des versions ; imports 1Password, Bitwarden, KeePass, CSV ; clés SSH et agent SSH ; envoi sécurisé ; Sentinelle en continu.
**Équipe et conformité** : stratégie d'organisation, journal d'activité exportable, accessibilité, anglais, modèles de documents juridiques.
**Sécurité** : nouvelle hiérarchie de clés (format 3), écran exclu des captures, presse-papiers hors historique, ligne de commande.

## 2.1.0 (Electron)

Connexion par Windows Hello, retrait de l'e-mail et des exemples, durcissement.
