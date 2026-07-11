# Audit Interaction Voie-Ouvrage — PWA

Deux versions equivalentes, memes resultats de calcul verifies (voir plus bas) :

- **pwa/** — version normale, code lisible (pour debug/maintenance)
- **pwa-obfuscated/** — meme application, JavaScript obfusque (pour deploiement public)

## Deploiement sur GitHub Pages

1. Creer un depot GitHub (ou en reutiliser un existant).
2. Copier le contenu d'UN SEUL des deux dossiers (`pwa/` ou `pwa-obfuscated/`) a la racine
   du depot (ou dans un sous-dossier, ex. `/docs`, selon votre configuration Pages) :
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `icons/icon-192.png`
   - `icons/icon-512.png`
   - `icons/apple-touch-icon.png`
3. Dans les parametres du depot GitHub : **Settings > Pages**, choisir la branche et le
   dossier source (`/` ou `/docs`).
4. L'application sera accessible a `https://<utilisateur>.github.io/<depot>/`.
5. Sur mobile (Safari/Chrome), l'option "Ajouter a l'ecran d'accueil" installera l'app en
   PWA (icone, plein ecran, fonctionnement hors-ligne apres une premiere visite).

Aucune modification n'est necessaire pour un depot de projet (sous-chemin
`/<depot>/`) : tous les chemins du manifest, du service worker et des icones sont
relatifs.

## Mise a jour du cache hors-ligne

Le service worker (`sw.js`) met en cache l'application au premier chargement. Apres un
nouveau deploiement, incrementez `CACHE_VERSION` dans `sw.js` (ex. `ivo-v1` -> `ivo-v2`)
pour forcer les navigateurs a recharger la nouvelle version plutot que de servir
l'ancienne depuis le cache.

## Verification de parite des resultats (obfuscation)

La version obfusquee a ete testee face a la version normale sur 4 scenarios couvrant
multi-travees, trafic LM71, appareil de dilatation, tassement d'appui, rail bloque/libre,
zone d'attaches et zone d'appareil de voie : convergence, nombre d'iterations et valeurs
de contrainte/glissement/deplacement identiques au 4e chiffre decimal pres sur tous les
scenarios. L'obfuscation (javascript-obfuscator : aplatissement de flux de controle,
tableau de chaines encode, injection de code mort) ne modifie aucun resultat de calcul.
