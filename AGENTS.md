# ChatGPT / Codex Instructions — Aziz Express

## Mémoire partagée
Lis `SHARED_MEMORY.md` avant de commencer toute action.
Ce fichier contient tout le contexte du projet (stack, pages, Firebase, décisions prises).
Après chaque action importante, mets à jour la section correspondante avec le préfixe `[YYYY-MM-DD ChatGPT]`.

## État Android à connaître
- `AzizGPS` utilise maintenant un login Firebase avant accès à l'écran principal
- `MainActivity` filtre les livraisons actives par `courierId == uid`
- Le bouton notification `Arrêter` du service GPS est corrigé côté Android
