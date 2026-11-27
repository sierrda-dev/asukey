# asukey

Gestionnaire de mots de passe **local** pour Windows 11, chiffré de bout en bout, sans compte en ligne.

**Dernière version : 0.2.0** (27 novembre 2026)

- **Installer** : [Microsoft Store](https://apps.microsoft.com/detail/9PNJ014KZP63) (conseillé : mises à jour automatiques)
- **Télécharger** : [https://sierrda-dev.github.io/asukey](https://sierrda-dev.github.io/asukey) (kit d'installation)
- **Déjà installé** (0.1.2 ou plus récent) : asukey propose les mises à jour tout seul.
- **Toutes les versions** : [Releases](https://github.com/sierrda-dev/asukey/releases) · [Journal des versions](CHANGELOG.md)

## Nouveautés de la 0.2.0

- **Couleur et icône des coffres** : clic droit sur un coffre › Couleur et icône… (8 couleurs, 12 icônes, avec aperçu). La couleur se retrouve partout : tuile et sélection dans la barre latérale, pastille sur les éléments quand la liste mélange plusieurs coffres, étiquette teintée dans la fiche, loupe de la recherche. Pour un coffre partagé, seul le propriétaire change la couleur ; l'icône, chacun la choisit pour soi. Masqué en contraste élevé (Windows impose ses couleurs).
- **Recherche rapide** (ex-Accès rapide) : le raccourci global (Ctrl+Maj+Espace), depuis n'importe quelle application, sans ouvrir asukey. Dans asukey, une seule recherche : la barre du haut (Ctrl+F ou Ctrl+K), avec ses suggestions. Sélection au style Windows 11, coffre de chaque élément, et des actions : générer un mot de passe (copié), mode présentation, ouvrir ou verrouiller asukey.
- **Fiche plus confortable** : un clic sur un champ le copie, avec « ✓ Copié » à la place de son intitulé ; les sites web rejoignent la carte de l'identifiant et du mot de passe ; titres de section sans capitales (style Windows 11) ; « Dernière modification hier à 15:11 » sans les secondes.
- **Réglages** : rubriques regroupées sous « Protection », « Données » et « Application », une icône par carte de réglage.
- **Zone de droite** quand rien n'est sélectionné : deux raccourcis cliquables (Ctrl+N, Ctrl+F) et les éléments ouverts récemment. **Aide** devient un bouton rond discret.
- **Sentinelle** : pastille de gravité sur chaque carte (Urgent, À faire, Conseil, Rangement) et icône dans sa couleur ; la dernière carte d'une ligne incomplète prend la place restante.
- **Page Partage** : ta photo partout où tu apparais (activité, membres), boutons Inviter, Ouvrir et Gérer côte à côte, activité limitée aux 5 dernières modifications avec un lien « Tout afficher ».
- **Confidentialité** (Réglages › Protection) : tout ce qui peut passer par Internet au même endroit (logos des sites, vérification des fuites, mises à jour, synchronisation), avec pour chaque fonction ce qui est envoyé et à qui ; et ce qui reste toujours sur l'ordinateur (extension, analyses de la Sentinelle, aucune statistique). Les logos des sites se règlent désormais ici.
- **« Se connecte avec »** pour les identifiants : Google, Apple, Microsoft, Facebook, GitHub… (ou saisie libre), pour se souvenir par où l'on s'est inscrit. Affiché dans la liste quand il n'y a pas de nom d'utilisateur, et compris par la recherche.
- **Extension : « Continuer avec Google »** : quand tu te connectes à un site avec Google, Apple, Microsoft, Facebook ou GitHub, l'extension propose au retour sur le site d'enregistrer le compte (« Se connecte avec Google »), sans mot de passe. Si un identifiant du site existe déjà sans mot de passe, le service y est simplement noté. Jamais de doublon, rien n'est proposé sur la page du service lui-même.
- **Initiales des éléments sans logo** : deux lettres sur un fond pastel propre à chaque site, plus lisibles qu'une seule lettre sur une couleur vive.
- **Survol d'un champ** (identifiant, mot de passe, site…) : la ligne se teinte, « Copier » apparaît à droite (un clic n'importe où sur la ligne copie) et un chevron ouvre les autres actions : Révéler, Afficher en gros caractères, Ouvrir le site. Une pastille en bas au centre dit ce qui a été copié (« Mot de passe copié »).
- **Passkeys dans la fiche** : une ligne « passkey · créée hier » dans la carte de l'identifiant, à côté du nom d'utilisateur, au lieu d'une section à part.
- **Filtre de catégories** : seulement les catégories présentes, avec leur nombre aligné à droite et une coche sur celle choisie, à jour à chaque ouverture.
- **Éditeur** : le coffre de destination, à côté d'« Enregistrer », prend la couleur et l'icône du coffre.
- **pCloud** : pas de connexion directe (pCloud a refusé l'accès à son API) ; code correspondant retiré. pCloud reste utilisable par son application pCloud Drive.
- **Publication sécurisée** (après l'incident 1Password de novembre 2026) : aucun identifiant cloud dans le code public (`CloudApps.Local.cs`, fichier local de l'éditeur ; sans lui, tout compile et les services restent « pas encore activés »), CI sans certificat ni secret, publication refusée si les identifiants cloud manquent, et `tools\verifier-publication.ps1` pour vérifier à tout moment que le site et la version GitHub sont exactement ce qui a été signé. Liste des comptes à protéger : `docs/SECURITE-PUBLICATION.md`.
- **Allègement** : retrait des fonctions développeur masquées depuis la 0.1.5.1 (ligne de commande, « Copier la référence », serveur MCP, extension VS Code, analyse de secrets dans le code, signature Git, import .env) et du code devenu inutile (161 textes, réglages et méthodes jamais utilisés). Les éléments « Environnement » existants restent lisibles et modifiables. Un hôte de test (`tests/Asukey.TestHost`, jamais livré) remplace la ligne de commande pour les tests de l'extension et le coffre de démonstration.
- **Mode présentation** (menu du compte, Ctrl+Maj+P, ou la recherche rapide) : pour une réunion, un tutoriel ou une capture. asukey redevient visible dans les partages d'écran, mais aucun secret ne peut s'afficher (pas de bouton Afficher, codes 2FA masqués, pas d'affichage en grand) ; copier et remplir fonctionnent toujours. Contour et halo ambrés autour de la fenêtre et rappel « Mode présentation » en haut, arrêt automatique au verrouillage, jamais enregistré.

## Installer

1. Télécharge `asukey-0.2.0-kit.zip` depuis la [dernière version](https://github.com/sierrda-dev/asukey/releases/latest).
2. Clic droit › **Extraire tout**, puis double-clic sur **Installer asukey**.
3. Windows demande d'approuver l'éditeur d'asukey une seule fois par ordinateur.

## Sécurité

Les paquets sont signés par le certificat [Coffre.cer](https://sierrda-dev.github.io/asukey/Coffre.cer) ; Windows refuse une mise à jour signée par un autre. Le site ne reçoit rien de ton coffre : l'application y lit seulement [version.json](https://sierrda-dev.github.io/asukey/version.json).

Ce dépôt contient le site de téléchargement et des mises à jour. Il est publié par `tools/release.ps1 -Publish`.
