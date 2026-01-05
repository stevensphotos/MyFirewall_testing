
Protocole de Test – MyFirewall (V0.9)
Objectif
Valider la stabilité, la sécurité et l’ergonomie de l’application MyFirewall sur des appareils Android (API 24 à 35).

1️⃣ Prérequis pour le testeur

📱 Un appareil Android physique (les émulateurs ne gèrent pas correctement le VPN et la biométrie).
🔑 Accès Root (optionnel, pour tester le filtre Hosts).
👆 Empreinte digitale ou code PIN configuré sur l’appareil.
🌐 Connexion Wi‑Fi et données mobiles fonctionnelles.


2️⃣ Test du Cycle de Vie et Sécurité
TestAction AttenduT.01 – Premier lancement (Onboarding)Installer et ouvrir l’application pour la première fois.L’écran d’onboarding s’affiche. Le bouton Start demande les permissions nécessaires. Aucun verrouillage biométrique n’est demandé à ce stade.T.02 – Verrouillage biométrique (App Lock)1. Activer Application Lock dans Settings.  2. Fermer l’application (tuer le processus) et la relancer.Une invite biométrique système apparaît immédiatement. L’interface reste masquée tant que l’authentification n’est pas réussie.Action : Annuler l’authentification.Attendu : L’application se ferme immédiatement (finish()).T.03 – Délai de verrouillage (Timeout)Authentifier l’accès, mettre l’application en arrière‑plan > 30 s, puis revenir.L’application redemande une authentification biométrique.

3️⃣ Test des Moteurs de Filtrage (Mutual Exclusivity)
T.04 – URL Filter (VPN)


Action : Aller à l’écran Rules, cocher les listes de blocage, vérifier sur l’écran Status le téléchargement effectif des listes et leur activation.


Attendu : Les listes se téléchargent sans erreur.


Action : Activer URL Filter VPN et accepter la demande de connexion VPN d’Android.


Attendu : L’icône VPN apparaît dans la barre de statut, le statut passe à Active.


Vérification : Tenter d’accéder à un domaine bloqué (ex. doubleclick.net).


Résultat : L’accès doit être refusé.


T.05 – Application Filter (Routage par App)


Action : Activer Application Filter.


Attendu : Le URL Filter VPN se désactive automatiquement (s’il était actif) et le service VPN redémarre proprement.


Action : Dans l’onglet Applications, interdire l’accès Wi‑Fi à un navigateur (ex. Chrome).


Attendu : Le navigateur ne charge plus de pages en Wi‑Fi mais fonctionne en données mobiles si le toggle correspondant est ON.


T.06 – Transition Root (Hosts)


Action : Activer URL Filter Root (appareil rooté requis).


Attendu : Le service VPN s’arrête immédiatement, une demande SU apparaît, le toggle Start on Boot passe à OFF.


Vérification : Ouvrir un terminal/root explorer et vérifier que /etc/hosts contient les domaines de la base de données.



4️⃣ Test de l’Interface Utilisateur (Accessibilité)
T.07 – Grandes polices (Font scaling)

Action : Dans les paramètres Android, régler la taille de police à 200 %.
Attendu :

Dans Settings, les commutateurs restent visibles à droite (pas de débordement).
Dans la barre de navigation, les libellés ne sont pas tronqués ; ils utilisent l’ellipse (…) ou restent sur une seule ligne.



T.08 – Thèmes et couleurs

Action : Basculer entre Light, Dark et System. Activer Pure Black.
Attendu : L’UI s’adapte instantanément. En mode Pure Black, le fond doit être #000000 (OLED).


5️⃣ Test de Persistance et Maintenance
T.09 – Start on Boot

Action : Activer un filtre VPN, cocher Start on Boot, puis redémarrer l’appareil.
Attendu : Après le déverrouillage (Direct Boot), le service VPN se lance automatiquement, sans intervention manuelle.

T.10 – Import / Export de règles

Action : Exporter les règles dans un fichier JSON, supprimer une règle manuellement, puis réimporter le fichier.
Attendu : Un Toast confirme l’importation, la base de données Room est mise à jour, les doublons sont gérés (remplacement).


6️⃣ Rapport d’anomalie (Template)
- **ID** : (ex. BUG‑001)
- **Sévérité** : (Bloquant / Majeur / Mineur)
- **Composant** : (VPN / UI / Root / Sécurité)
- **Étapes de reproduction** :
- **Résultat observé** :
- **Résultat attendu** :
- **Logs (Logcat)** : (Optionnel mais recommandé pour les erreurs PermissionMonitor)

Protocole de Test – MyFirewall (V1.0) – Version synthétique
Objectif
Valider l’intégrité du filtrage réseau, la persistance des données Room et l’accessibilité de l’interface.

1️⃣ Tests UI & Navigation
1.1 Navigation & Pager


Action : Swiper entre les onglets Status, Applications, Rules et Settings.


Attendu : Transition fluide, le label de l’onglet sélectionné dans le NavigationSuiteScaffold est mis en évidence.


Test accessibilité : Augmenter la police système à 200 %; les labels de navigation ne doivent pas créer d’orphelins ni déborder (plafond ≈ 1.2×).


1.2 Sélection par long‑click (contextuelle)


Action : Dans Applications, faire un appui long sur une appli.


Attendu : Ouverture immédiate des Détails de l’application dans les paramètres Android.


Action : Dans Custom Rules, faire un appui long sur un domaine.


Attendu : Mode sélection activé, permettant suppression/groupée ou modification.


Action : Dans Settings régler la langue sur Français


Attendu : toute l'interface est en Français. Menus, textes, dialogs, toasts



2️⃣ Tests des moteurs de filtrage (VPN ↔ Hosts)
2.1 Filtrage URL via VPN


Action : Activer URL Filter VPN dans Settings.


Attendu : Demande d’autorisation VPN, icône VPN apparaît.


Validation : Accéder à un domaine présent dans la liste de blocage via un navigateur → requête échoue (NXDOMAIN).


2.2 Filtrage URL via Hosts (Root)


Action : Activer URL Filter Root.


Attendu :

Désactivation automatique du VPN (exclusivité).
Demande de permission SuperUser (SU).
Toggle Start on Boot passe à OFF.



Validation : cat /etc/hosts montre les règles injectées depuis la base Room.


2.3 Transition VPN → Hosts

Action : Passer rapidement de l’un à l’autre.
Attendu : Aucun race condition. Le délai (delay(400)) permet au system_server de libérer l’interface tun0 avant que le moteur Hosts ne prenne le relais.


3️⃣ Test pare‑feu (blocage par application)
3.1 Blocage de trafic sortant


Action : Activer Application Filter.


Action : Dans la liste, désactiver l’icône Wi‑Fi pour une appli (ex. YouTube).


Attendu : L’appli ne charge plus de données en Wi‑Fi.


Action : Désactiver également l’icône Mobile Data.


Attendu : L’appli est totalement isolée du réseau.


Vérification technique : Les logs montrent que le VpnPacketThread traite les paquets de l’UID concerné.



4️⃣ Import / Export de listes
4.1 Exportation

Action : Cliquer sur Export → Application Rules.
Attendu : Sélecteur de fichier SAF s’ouvre, le fichier JSON généré est valide et contient les colonnes packageName, wifiAllowed, etc.

4.2 Importation & validation JSON


Action : Importer un fichier JSON malformé ou avec un packageName invalide.


Attendu : Le filtre Regex rejette l’entrée, aucun crash.


Action : Importer un fichier valide.


Attendu : Transaction Room atomique, un Toast indique le nombre de règles importées.



5️⃣ Gestion des listes Custom (Blacklist / Whitelist)
5.1 Ajout de domaines personnalisés


Action : Ajouter un domaine manuellement dans Custom Rules.


Attendu : Validation du format (pas de caractères spéciaux interdits).


Action : Cliquer sur Sauvegarder.


Attendu : Si le VPN est actif, l’action ACTION_RELOAD_RULES est envoyée immédiatement pour rafraîchir le cache blockedDomains du service.



6️⃣ Tests de sécurité (biométrie)
6.1 Verrouillage au démarrage


Action : Activer Application Lock, tuer l’app, la relancer.


Attendu : BiometricPrompt s’affiche avant tout accès UI.


Action : Annuler l’authentification.


Attendu : L’app appelle finish() et se ferme.


6.2 Timeout de session

Action : Déverrouiller l’app, la mettre en arrière‑plan > 30 s, puis revenir.
Attendu : LifecycleObserver détecte le dépassement du lockTimeout et redemande l’empreinte.


📋 Checklist finale – Rapport de stabilité

Aucun blocage du thread principal (ANR) lors des écritures SharedPreferences.apply().
Le thread VPN consomme < 2 % CPU en veille.
Les icônes s’affichent correctement en mode Dark et Pure Black.
Pas de fuite mémoire lors du changement d’orientation (rememberSaveable).


Vous pouvez copier‑coller ce contenu dans un fichier README.md (ou tout autre fichier .md) et il sera correctement rendu dans n’importe quel visualiseur Markdown.
