 # Aziz Express 🛵

  > Plateforme de livraison locale pour coursier indépendant — Oujda, Maroc

  **Live demo:** https://ilyas8888.github.io/aziz-express

  ---

  ## Aperçu

  Application web complète de gestion de livraisons, construite pour un vrai
  coursier indépendant. Permet aux clients de passer des commandes, au coursier
  de gérer ses livraisons en temps réel, et à l'admin de piloter l'activité.

  ---

  ## Fonctionnalités

  - **Commande publique** — formulaire client avec estimation des frais, annulation 60s, envoi WhatsApp automatique
  - **Tracking GPS temps réel** — position du coursier mise à jour toutes les 5s via Firebase
  - **Dashboard admin** — gestion des demandes, livraisons en cours, stats financières
  - **Historique filtré par rôle** — admin voit tout, coursier voit seulement les siennes
  - **Stats & graphiques** — bénéfice/livraisons sur 7j/30j/tout, top clients (Chart.js)
  - **QR Code imprimable** — pour marketing terrain chez les commerçants partenaires
  - **Gestion multi-coursiers** — création/suppression de comptes coursiers
  - **App Android native** — GPS en foreground service, fonctionne écran verrouillé

  ---

  ## Stack technique

  | Couche | Technologie |
  |--------|-------------|
  | Frontend | HTML / CSS / JavaScript vanilla |
  | Base de données | Firebase Realtime Database |
  | Auth | Firebase Authentication |
  | Cartes | Leaflet.js + OpenStreetMap |
  | Itinéraires | OSRM (open source, sans clé API) |
  | Hosting | GitHub Pages |
  | App mobile | Android (Java) — foreground service GPS |

  ---

  ## Architecture

  Client (order.html) ──► Firebase Realtime DB ◄── Dashboard admin
                                │
                      Coursier (courier.html)
                                │ GPS toutes les 5s
                      Client tracking (track.html)

  ---

  ## Screenshots
  
  <img width="1365" height="598" alt="image" src="https://github.com/user-attachments/assets/5bef2277-7b54-4a1b-b07e-5467b7a0237f" />
  <img width="370" height="579" alt="image" src="https://github.com/user-attachments/assets/6690d639-a5cb-42b5-8037-e84cb1a60bc6" />
  <img width="1365" height="590" alt="image" src="https://github.com/user-attachments/assets/595d3602-e4da-4e71-8e85-c359acfcd0d9" />
  <img width="201" height="434" alt="image" src="https://github.com/user-attachments/assets/ea6b4af1-9c81-4d20-96eb-f4fb59b67240" />


  ---

  ## Lancer en local

  Aucune installation requise. Ouvrir `index.html` dans un navigateur.

  > Firebase est déjà configuré et connecté au projet de production.

  ---

  ## Projet

  Construit pour **Aziz**, coursier indépendant à Oujda — dans le but de
  remplacer les plateformes tierces et de travailler directement avec ses clients.

  ---

  *Développé par [ilyas8888](https://github.com/ilyas8888)*

  ---
