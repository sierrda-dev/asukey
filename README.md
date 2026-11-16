# Coffre

Gestionnaire de mots de passe **local** pour Windows 11 et macOS, chiffré de bout en bout, sans compte en ligne.

**Dernière version : 0.1.5.1** (16 novembre 2026)

- **Télécharger** : [https://sierrda-dev.github.io/coffre](https://sierrda-dev.github.io/coffre) (kit d'installation et version portable)
- **Déjà installé** (0.1.2 ou plus récent) : Coffre propose les mises à jour tout seul.
- **Toutes les versions** : [Releases](https://github.com/sierrda-dev/coffre/releases) · [Journal des versions](CHANGELOG.md)

## Nouveautés de la 0.1.5.1

**Apparence personnalisable**
- **Nouvelle icône** : disque bleu-violet avec trou de serrure, entouré d'un anneau, sur Windows (barre des tâches, menu Démarrer, Store), dans l'extension de navigateur et sur Mac. Aux petites tailles, seul le disque est gardé pour rester net.
- Nouvelle rubrique **Réglages › Apparence** : thème (comme Windows, clair, sombre), densité **Confortable** ou **Compact** (lignes de la liste et de la barre latérale plus serrées), taille de l'interface de 80 à 150 % (boutons − et +, ou Ctrl+= et Ctrl+−, Ctrl+0 pour revenir à 100 %), et « Rétablir les valeurs par défaut ». Tout s'applique immédiatement, sans redémarrer.
- **Barre latérale** : choisis les rubriques toujours affichées (Catégories, Tags) et, en option, le nombre d'éléments à côté de chaque rubrique.
- **Couleur de la barre latérale** : neuf teintes (Brume, Lavande, Menthe, Sable, Pétale, Ardoise, Nuit, Prune, Forêt) ou une couleur personnalisée ; le texte passe en clair ou en foncé selon la couleur.
- **Couleur d'accent** : bleu de Coffre ou huit autres couleurs, ou une couleur personnalisée, pour les boutons, la sélection et les liens.
- **Installer l'extension de navigateur depuis Coffre** : menu ⋯ › « Installer l'extension de navigateur… » (ou Réglages › Navigateur). Choisis Chrome, Edge, Brave ou Firefox : Coffre prépare l'extension (livrée avec l'application), copie le chemin, ouvre la page des extensions du navigateur, affiche les deux derniers clics et le code d'association dans la même fenêtre. L'extension installée est actualisée toute seule à chaque mise à jour de Coffre.
- **Quitter Coffre** depuis le menu ⋯ de la barre latérale et le menu du compte (Ctrl+Q) : le coffre est verrouillé puis l'application se ferme.
- La rubrique **Développeur** est retirée de la barre latérale, des réglages et de la Sentinelle (les fonctions restent dans le code pour plus tard).
- Pièce jointe sur n'importe quel élément : menu ⋮ de la fiche › « Ajouter une pièce jointe… ».

## Installer

1. Télécharge `Coffre-0.1.5.1-kit.zip` depuis la [dernière version](https://github.com/sierrda-dev/coffre/releases/latest).
2. Clic droit › **Extraire tout**, puis double-clic sur **Installer Coffre**.
3. Windows demande d'approuver l'éditeur de Coffre une seule fois par ordinateur.

## Sécurité

Les paquets sont signés par le certificat [Coffre.cer](https://sierrda-dev.github.io/coffre/Coffre.cer) ; Windows refuse une mise à jour signée par un autre. Le site ne reçoit rien de ton coffre : l'application y lit seulement [version.json](https://sierrda-dev.github.io/coffre/version.json).

Ce dépôt contient le site de téléchargement et des mises à jour. Il est publié par `tools/release.ps1 -Publish`.
