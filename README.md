# asukey

Gestionnaire de mots de passe **local** pour Windows 11, chiffré de bout en bout, sans compte en ligne.

**Dernière version : 0.1.7** (23 novembre 2026)

- **Télécharger** : [https://sierrda-dev.github.io/coffre](https://sierrda-dev.github.io/coffre) (kit d'installation)
- **Déjà installé** (0.1.2 ou plus récent) : asukey propose les mises à jour tout seul.
- **Toutes les versions** : [Releases](https://github.com/sierrda-dev/coffre/releases) · [Journal des versions](CHANGELOG.md)

## Nouveautés de la 0.1.7

**Première version pour le Microsoft Store**
- asukey arrive sur le **Microsoft Store** : installation en un clic, sans certificat à approuver, mises à jour par le Store. La version du kit sur GitHub reste disponible, avec les mêmes fonctions.
- Passer du kit au Store est sans perte : au premier lancement, la version du Store reprend tes réglages, puis propose d'ouvrir la page de l'ancienne version dans les Paramètres de Windows pour la désinstaller. Ton coffre, dans Documents, ne bouge pas.
- Dans la version du Store, les messages qui parlaient du kit d'installation renvoient vers le Microsoft Store (installer asukey sur un autre ordinateur, réinstaller l'extension).
- Les logos ne sont plus demandés pour les adresses réservées qui n'existent pas sur Internet (`.example`, `.test`, `.invalid`, `.home.arpa`…).
- L'aide pour ajouter un appareil ne mentionne plus de version de test pour iPhone.
- Pour l'éditeur : `tools\store.ps1` retient l'identité du Store après la première fois, `asukey demo` crée un coffre de démonstration entièrement inventé pour les captures d'écran, et `docs/STORE.md` contient toute la soumission (fiches en français et en anglais, classification, remarques pour la certification).

## Installer

1. Télécharge `asukey-0.1.7-kit.zip` depuis la [dernière version](https://github.com/sierrda-dev/coffre/releases/latest).
2. Clic droit › **Extraire tout**, puis double-clic sur **Installer asukey**.
3. Windows demande d'approuver l'éditeur d'asukey une seule fois par ordinateur.

## Sécurité

Les paquets sont signés par le certificat [Coffre.cer](https://sierrda-dev.github.io/coffre/Coffre.cer) ; Windows refuse une mise à jour signée par un autre. Le site ne reçoit rien de ton coffre : l'application y lit seulement [version.json](https://sierrda-dev.github.io/coffre/version.json).

Ce dépôt contient le site de téléchargement et des mises à jour. Il est publié par `tools/release.ps1 -Publish`.
