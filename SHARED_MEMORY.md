# Shared Memory — Claude & ChatGPT
# Projet : Aziz Express (app livraison Oujda)

> Lu et mis à jour par Claude et ChatGPT à chaque session.

---

## Contexte projet
Application de livraison pour le cousin Aziz (Oujda) — livreur moto indépendant.
But : indépendance totale des plateformes (Glovo etc.), clients directs.
Aziz gagne via frais livraison + 20% des marchands.

**Live :** https://ilyas8888.github.io/aziz-express
**Code :** C:\Claude\OUJDA-LIVRAISON
**App Android :** C:\Users\ilyas\AndroidStudioProjects\AzizGPS — GitHub: https://github.com/ilyas8888/aziz-gps

---

## Stack technique
- Frontend : HTML/CSS/JS vanilla
- Hosting : GitHub Pages
- DB temps réel : Firebase Realtime Database (projet: rent-4db84, région: europe-west1)
- Auth : Firebase Email/Password
- Maps : Leaflet.js + OpenStreetMap
- Routing : OSRM (gratuit, sans clé API)
- Brand : Orange #FF5A1F, Navy #0F172A, Warm white #FFF5F0, Police : Poppins

---

## Pages existantes
| Fichier | Rôle |
|---|---|
| index.html | Landing page |
| login.html | Auth (coursier/admin uniquement) |
| dashboard.html | Admin : tout voir + demandes + stats. Coursier : ses livraisons seulement |
| history.html | Historique filtré par rôle |
| courier.html | Démarrer livraison, GPS, taguée courierId/courierName |
| track.html | Page client publique : carte fullscreen, route, ETA, distance, statut |
| order.html | Formulaire public : save Firebase + WhatsApp + annulation 60s + estimation frais |
| contacts.html | Liste contacts Firebase avec épinglage position |
| stats.html | KPIs, graphiques 7j/30j/tout, top clients (Chart.js) |
| qrcode.html | QR Code vers order.html, imprimable, admin seulement |
| admin-couriers.html | Créer/supprimer comptes coursiers (secondary Firebase app) |
| firebase-config.js | Firebase init + db |

---

## Système de rôles Firebase
- `users/{uid}` → { name, email, phone, role: 'admin' | 'courier' }
- Admin voit tout, coursier voit seulement ses livraisons (filtre JS côté client)
- Firebase Rules protègent users/ contre auto-promotion admin
- Livraisons taguées : courierId + courierName

---

## Firebase Rules (Realtime DB)
- users/$uid : write = seulement si nœud n'existe pas OU si caller est admin
- livraisons, demandes, contacts, _ping : auth != null
- track.html et order.html : publics (pas d'auth requise)
- `.indexOn: ["active"]` sur livraisons (query orderByChild)

---

## Tarifs livraison (order.html)
- < 1 km → 15 DH
- 1–5 km → 10 DH/km
- 5–8 km → 8 DH/km
- > 8 km → 65 DH (max)

---

## App Android AzizGPS
- Package : com.azizexpress.gps
- Foreground Service GPS — fonctionne écran verrouillé
- Détecte automatiquement la livraison active (active: true) depuis Firebase
- Envoie lat/lng/timestamp toutes les 5s
- SharedPreferences pour restaurer l'état
- Login Firebase email/password ajouté avant accès à l'app
- MainActivity filtre maintenant les livraisons actives par `courierId == uid`
- Bouton notification `Arrêter` corrigé : action `STOP` gérée dans `GpsService`
- **Déploiement :** Build → Build APK → envoyer via WhatsApp à Aziz
- **Permissions téléphone Aziz :** Localisation → "Autoriser en permanence" + Batterie → "Non restreinte"

---

## Comptes Firebase
- Admin Aziz : ilyassboulouiz@outlook.com, uid: 2hIPGekfC9c7V7fn6auk090ves93
- Coursier test Karim : KarimBen@outlook.com, uid: 9cnZxYUcYJSK1R8hqauQUkZLE5U2
- WhatsApp Aziz : +212616937149

---

## Décisions techniques prises
- Push notifications annulées — WhatsApp suffit pour notifier Aziz
- Wake Lock retiré — trop gourmand en batterie
- Dashboard keepalive : ping 30s + visibilitychange
- App Android choisie (pas React Native/Flutter) — plus légère, GPS natif
- Filtre historique côté JS (pas Firebase rules) — acceptable car coursiers de confiance
- BASE path detection pour GitHub Pages subdirectory

---

## Bugs corrigés
- track.html : livreur n'apparaissait pas → Firebase Rules livraisons: ".read": true
- App Android : même cause rules + onCancelled vide avalait l'erreur silencieusement
- App Android : démarrage GPS automatique dès qu'une livraison active est détectée
- App Android : bouton notification `Arrêter` fonctionne désormais
- App Android : bug futur multi-coursier corrigé via authentification Firebase + filtre `courierId == uid`

---

## Ce qui reste à faire
- Tester en conditions réelles (checklist complète)
- Multi-courier : push livraison d'un livreur à un autre
- QR Code : ajouter nom/logo du commerce partenaire
- Sécurité historique : restructurer livraisons/{courierId}/{id} pour vrai filtre Firebase

---

## Préférences développeur
- Ne jamais faire de grosses modifications automatiques (>3k tokens)
- Donner des blocs "chercher / remplacer" pour VS Code (Ctrl+F)
- Donner des commandes shell à exécuter manuellement
- Rester concis, économiser les tokens

---

## Notes from Claude
[2026-04-22 Claude] Session Android : fix bouton "Arrêter" notification (GpsService.kt — action STOP géré dans onStartCommand), ajout LoginActivity (login Firebase email/password), MainActivity filtre livraisons par courierId == uid, bouton Déconnexion ajouté. Dépendance firebase-auth-ktx 22.3.1 ajoutée. LoginActivity devient le launcher dans AndroidManifest. Prochaine étape : Sync Gradle → Build APK → tester sur téléphone Aziz.

## Notes from ChatGPT
<!-- [YYYY-MM-DD ChatGPT] -->
[2026-04-22 ChatGPT] Session started. Read AGENTS.md and SHARED_MEMORY.md. Ready to assist on Aziz Express project.
[2026-04-22 ChatGPT] Updated shared memory after confirmed Android fixes: notification STOP action handled, LoginActivity added, active deliveries filtered by courierId == uid, and next manual step is Sync Gradle then Build APK in Android Studio.
