# asukey

Gestionnaire de mots de passe **local** pour Windows 11, chiffré de bout en bout, sans compte en ligne.

**Dernière version : 0.1.6** (19 novembre 2026)

- **Télécharger** : [https://sierrda-dev.github.io/coffre](https://sierrda-dev.github.io/coffre) (kit d'installation)
- **Déjà installé** (0.1.2 ou plus récent) : asukey propose les mises à jour tout seul.
- **Toutes les versions** : [Releases](https://github.com/sierrda-dev/coffre/releases) · [Journal des versions](CHANGELOG.md)

## Nouveautés de la 0.1.6

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

## Installer

1. Télécharge `asukey-0.1.6-kit.zip` depuis la [dernière version](https://github.com/sierrda-dev/coffre/releases/latest).
2. Clic droit › **Extraire tout**, puis double-clic sur **Installer asukey**.
3. Windows demande d'approuver l'éditeur d'asukey une seule fois par ordinateur.

## Sécurité

Les paquets sont signés par le certificat [Coffre.cer](https://sierrda-dev.github.io/coffre/Coffre.cer) ; Windows refuse une mise à jour signée par un autre. Le site ne reçoit rien de ton coffre : l'application y lit seulement [version.json](https://sierrda-dev.github.io/coffre/version.json).

Ce dépôt contient le site de téléchargement et des mises à jour. Il est publié par `tools/release.ps1 -Publish`.
