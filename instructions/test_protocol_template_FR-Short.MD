# 🧪 Protocole de Test Utilisateur - MyFirewall

Ce document contient une série de tests simples pour vérifier que **MyFirewall** protège correctement votre appareil. Aucun bagage technique n'est requis.

## 📋 Avant de commencer
*   **Version de l'app :** v1.0.0 (ou plus récente)
*   **Connexion :** Wi-Fi ou Données Mobiles active.
*   **Important :** Si vous utilisez un autre VPN (ex: NordVPN), déconnectez-le avant de tester MyFirewall.

---

## 🟢 Étape 1 : Premier lancement et Configuration
**Objectif :** Vérifier que l'application s'installe et se configure sans erreur.

1.  **Ouvrez l'application** pour la première fois.
2.  **Parcourez l'écran de bienvenue** et le guide de démarrage rapide.
3.  **Permissions :** Acceptez les demandes de notifications et de statistiques d'utilisation lorsqu'elles apparaissent.
4.  **Finalisation :** Cliquez sur "Démarrer".

**Résultats attendus :**
- [ ] Le tableau de bord (Dashboard) s'affiche correctement.
- [ ] Le statut indique que la protection est prête à être activée.

---

## 🟢 Étape 2 : Test du Pare-feu (Blocage d'Application)
**Objectif :** Vérifier que l'on peut couper l'accès internet d'une application spécifique.

1.  Allez dans l'onglet **Applications**.
2.  Choisissez une application qui utilise internet (ex: **YouTube** ou **Chrome**).
3.  Appuyez sur les icônes **Wi-Fi** et **Données Mobiles** pour qu'elles deviennent **grises** (bloquées).
4.  Allez dans Parametres et activez Pare-feu Applications, acceptez la demande de connexion pour configurer une connexion VPN
5.  Ouvrez l'application choisie et essayez de charger une vidéo ou une page web.

**Résultats attendus :**
- [ ] L'application doit afficher un message d'erreur ("Hors ligne" ou "Pas de connexion").
- [ ] Revenez dans MyFirewall, débloquez-la (icônes redevenues grises/bleues) : l'application doit refonctionner immédiatement.

---

## 🟢 Étape 3 : Test du Filtre URL (Anti-Publicité)
**Objectif :** Vérifier que le blocage des publicités (DNS) fonctionne.

1.  Allez dans l'onglet **Règles**.
2.  Activez l'option **Publicités et Traceurs**.
3.  Vous pouvez vérifier sur l'écran Statut, le téléchargement des règles 
4.  Allez dans l'écran Parametres et activezFiltres d'URL basé sur VPN
5.  Ouvrez votre navigateur et rendez-vous sur le site suivant: https://adblock.turtlecute.org 
6.  Observez le score de blocage
7.  
**Résultats attendus :**
- [ ] Le scored de blocage doit dépasser 60% avec la liste de blocage Pubs et traceurs
- [ ] Sur d'autres sites, la navigation semble plus fluide.

---

## 🟢 Étape 4 : Sécurité et Verrouillage
**Objectif :** Vérifier que l'accès à vos réglages est protégé.

1.  Allez dans l'onglet **Paramètres**.
2.  Activez l'option **Verrouillage de l'application**.
3.  Fermez l'application (enlevez-la des applications récentes).
4.  Relancez MyFirewall.

**Résultats attendus :**
- [ ] MyFirewall demande votre empreinte digitale, votre visage ou votre code PIN avant d'ouvrir le Dashboard.

---

## 🟢 Étape 5 : Surveillance en temps réel
**Objectif :** Vérifier que les statistiques affichées sont correctes.

1.  Sur l'écran **Dashboard**, observez le compteur "Applications bloquées".
2.  Lancez une application autorisée (ex: Instagram) et faites défiler du contenu.
3.  Revenez rapidement sur le Dashboard de MyFirewall.

**Résultats attendus :**
- [ ] Le graphique de vitesse (Vitesse de trafic) doit montrer des pics d'activité.
- [ ] Les compteurs Wi-Fi ou Mobiles doivent avoir augmenté de quelques Ko/Mo.

---

## 🟢 Étape 6 : Interface utilisateur
**Objectif :** Vérifier que l'affichage fonctionne correctement.

1.  Parcourrez les écrans, vérifiez que les pages de l'application s'affichent correctement, basculez votre appareil pour forcer l'affichage horizontal.
2.  Dans les parametres selectionnez une langue différente de l'Anglais, comme le Français, vérifiez les menus, les toasts, les dialogues

**Résultats attendus :**
- [ ] L'affichage ne doit pas présenter d'anomalies, (menus coupés, switches coupés) lors de la rotation de l'écran l'affichage doit réagir immédiatement.
- [ ] Lorsque la langue selectionnée est le Français, tous les textes, menu ou toasts doivent etre affichés en Français.

## 🛠 Que faire si un test échoue ?

Si vous remarquez un comportement anormal, vérifiez les points suivants avant de signaler un bug :
1.  **Notification :** Vérifiez qu'une petite icône de clé ou de l'application est bien présente dans la barre de notifications en haut de votre téléphone.
2.  **DNS Privé :** Dans les réglages de votre téléphone (Connexions > Plus de paramètres), assurez-vous que le "DNS Privé" est réglé sur **"Désactivé"**.
3.  **Mode Économie d'énergie :** Parfois, Android ferme les applications de sécurité pour économiser la batterie. Désactivez l'optimisation de batterie pour MyFirewall si nécessaire.

---
*Fin du protocole de test.*
