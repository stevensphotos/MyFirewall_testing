# 🛡️ Mode d'emploi : MyFirewall

## Introduction
MyFirewall est une solution de protection de la vie privée et de contrôle réseau pour Android. Elle permet de bloquer les publicités, les traceurs et de contrôler précisément l'accès Internet de chaque application installée, que votre appareil soit rooté ou non.

---

## 🔑 Les Permissions (Écran Onboarding)
Lors du premier démarrage, MyFirewall nécessite plusieurs autorisations critiques pour fonctionner :

*   **Service VPN (Local)** : Utilisé pour intercepter le trafic sans envoyer vos données à un serveur externe.
*   **Statistiques d'utilisation (optionnel)** : Permet d'identifier quelle application consomme des données en temps réel.
*   **Notifications** : Indispensable pour maintenir le service actif en arrière-plan et vous alerter en cas de déconnexion.
*   **Accès Root (Optionnel)** : Permet un filtrage de bas niveau via le fichier `hosts` système, offrant de meilleures performances et une consommation de batterie nulle.

---

## 1. Écran Dashboard (Status)
Cet écran centralise l'état de votre protection.

*   **Surveillance** : Visualisez le nombre d'applications bloquées et la vitesse actuelle du trafic (Upload/Download).
*   **Cartes des règles (Filtres URL)** :
    *   **Appui prolongé** : Permet d'activer ou de désactiver instantanément une catégorie de filtrage (Publicités, Réseaux Sociaux, etc.) directement depuis le tableau de bord sans passer par les réglages.

---

## 2. Écran Applications
Gérez les droits d'accès réseau de chaque application individuellement.

### 2.1 Catégories et Filtres rapides
*   **Icônes de filtrage** : En haut de la liste, des icônes permettent d'isoler les applications (Toutes, Système, Utilisateur, Accès Internet, Pas d'accès Internet).
*   **Appui prolongé sur une icône de filtre** : Sélectionne ou désélectionne rapidement toutes les applications correspondant à ce filtre pour une gestion groupée.

### 2.2 Contrôle par application
*   **Clic sur l'icône de l'application** : Ouvre les propriétés système de l'application (pour vider le cache ou forcer l'arrêt).
*   **Appui prolongé sur le nom de l'application** : Bascule instantanément toute la connectivité (ON/OFF). Si l'application était autorisée, elle devient totalement bloquée, et inversement.
*   **Fonctionnement des icônes de flux** :
    *   🌐 **Wi-Fi** : Autorise/Bloque l'accès lorsque vous êtes sur un réseau sans fil.
    *   📶 **Mobile Data** : Autorise/Bloque l'accès sur les réseaux 4G/5G.
    *   ✈️ **Roaming** : Bloque spécifiquement l'accès lorsque vous êtes à l'étranger pour éviter les frais de hors-forfait.

---

## 3. Écran Rules (Règles de filtrages par nom de domaines)
Configurez votre moteur de blocage DNS.

### 3.1 Sélections des listes (Presets)
*   **Provenance** : Les listes proviennent de sources reconnues (StevenBlack, AdAway,).
*   **Mises à jour** : MyFirewall vérifie périodiquement la fraîcheur des listes. Vous pouvez forcer une mise à jour manuelle pour obtenir les derniers domaines malveillants répertoriés.

### 3.2 User Blocklist (Édition Manuelle)
*   **Édition** : Ecrivez, Copiez/collez vos propres domaines à bloquer dans le champ texte (un par ligne).
*   **Bouton Clear** :
    *   *Appui simple* : Vide le champ de texte actuel pour une nouvelle saisie. Appui simple* : Vide le champ de texte actuel pour une nouvelle saisie.
    *   Le bouton Configurer recharge dans l'éditeur les règles présentes dans la base de données.
    *   *Via menu déroulant* : Permet de supprimer définitivement toutes les règles personnalisées enregistrées dans la base de données.
*   **Export local** : Utilisez le boutons dédiés pour exporter vos règles vers un fichier `.txt`

### 3.3 Écran Import / Export (Global)
*   **Bouton Exporter** : Sauvegarde votre configuration complète.
    *   **Menu déroulant** : Permet d'exporter sélectivement soit les règles d'applications (Pare-feu), soit les listes de filtrage URL.
*   **Bouton Importer** : Applique la même logique pour restaurer sélectivement vos réglages à partir d'une sauvegarde précédente.

---

## 4. Écran Settings (Paramètres)
Le cœur de la configuration technique.

### 4.1 Appareils non-rootés
Sur ces appareils, le filtrage utilise le moteur VPN local.
*   **Exclusivité** : Le filtrage d'URL et le filtrage d'applications sont exclusifs. Vous devez choisir quel moteur est prioritaire pour la gestion du tunnel VPN.

### 4.2 Appareils rootés
*   **Cumul** : Les règles sont cumulatives. Vous pouvez utiliser le moteur **Hosts** pour le filtrage d'URL (DNS) et le moteur **VPN** pour le filtrage d'applications, offrant une protection double couche ultra-performante.

### 4.3 Serveur DNS Custom
*   **Non-Root** : Vous pouvez spécifier un serveur DNS personnalisé (ex: Cloudflare, Quad9) directement dans l'application.
*   **Root** : Le DNS doit être réglé directement dans les paramètres système d'Android pour utiliser un serveur DNS personnalisé.

### 4.4 Notification et filtrage Hosts
*   **Filtrage URL Hosts** : Un service dédié s'occupe de l'écriture sécurisée du fichier hosts système, ou le systemless hosts de Magisk.
*   **Indépendance** : Une fois que le fichier `hosts` est écrit par MyFirewall, le blocage devient natif. Même si l'application est fermée, ou désinstallée, le système Android continuera de bloquer les domaines, ce qui est la méthode la plus économe en batterie.
* Pour éviter de se retrouver avec un fichier hosts modifé, et par exemple l'application desinstallée, une notification est pévue pour avertir l'utilisateur que la protction reposant sur le fichier hosts est active. Pour permettre l'affichage de celle-ci, il est nécesaire de désactiver l'optimisation de la batterie pour autoriser l'utilisation en arrière-plan sans restrictions de l'application, afin de ne pas tuer le service d'affichage de la notification.

### 5 MyFirewall pour utilisateurs avancés

### 5.1 Utilisation avec un VPN tiers (ex: NordVPN, ProtonVPN)
Android possède une limitation logicielle : **un seul service VPN peut être actif à la fois** sur l'ensemble du système. Comme MyFirewall utilise un VPN local pour le filtrage d'applications et d'URLs (sur appareils non-rootés), le lancement d'un VPN commercial désactivera automatiquement la protection de MyFirewall.

*   **Appareils Non-Rootés :** Vous devez choisir entre la protection MyFirewall ou votre VPN. Ils ne peuvent pas fonctionner simultanément.
*   **Appareils Rootés :** C'est le mode recommandé pour les utilisateurs de VPN tiers. En utilisant le moteur **Hosts** pour le filtrage d'URLs, MyFirewall n'utilise pas le service VPN d'Android. Vous pouvez donc bénéficier du blocage des publicités de MyFirewall **ET** de la connexion sécurisée de votre VPN habituel en même temps.

### 5.1 A propos des presets

* Plusieurs fonctionnalités proposent des presets (regles de filtrage et serveur DNS). Si vous ne souhaitez pas les utiliser, Ωzzz
* il suffit de les désactiver, et d'utilser vos préférences à leur place. Ainsi la seule activité de l'application sur le réseau sera de filtrer les URLs et bloquer le traffic des applications.


### ⚠️ Note importante pour les utilisateurs Root. Si vous décidez de désinstaller MyFirewall, il est **impératif** de suivre ces étapes pour restaurer votre système à son état d'origine :

1.  **Désactivez toutes les listes de blocage** (Presets et User Blocklist) dans l'onglet "Rules".
2.  **Désactivez le "Filtrage d'URL (Hosts)"** dans l'écran "Paramètres".
3.  Cette action déclenche la routine de nettoyage qui **restaure le fichier `hosts` original** de votre appareil.

*Note : Si vous désinstallez l'application sans effectuer ces étapes, les domaines publicitaires resteront bloqués indéfiniment sur votre appareil, car la modification du fichier système est permanente.*

---
*MyFirewall - Votre vie privée, vos règles.*
