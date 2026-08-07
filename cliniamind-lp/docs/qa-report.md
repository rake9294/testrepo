# QA — landing page ClinIAMind (draft)

Tests exécutés avec Chromium (Playwright) sur `index.html` en `file://`.
Chaque scénario parcourt toute la page de haut en bas avant de mesurer, puis
remonte, pour reproduire un vrai parcours de lecture.

## Résultats

| Scénario | Débordement horizontal | Contenu resté masqué | Barres de progression | Erreurs console |
|---|---|---|---|---|
| Desktop 1440×900 | aucun (`scrollWidth` = `clientWidth` = 1440) | 0 | 100 / 100 / 75 / 45 % ✅ | 1 (voir note) |
| Mobile 390×844 | aucun (390 = 390) | 0 | 100 / 100 / 75 / 45 % ✅ | 1 (voir note) |
| `prefers-reduced-motion: reduce` | aucun | 0 | remplies d'emblée ✅ | 1 (voir note) |
| JavaScript désactivé | aucun | 0 | — | — |

> **Note sur l'erreur console** : `ERR_CONNECTION_RESET` sur Google Fonts.
> L'environnement de build n'a pas d'accès réseau sortant depuis le navigateur.
> Les polices se chargeront normalement chez toi ; les piles de repli
> (`ui-sans-serif`, `Georgia`) sont en place et la page reste correcte sans elles.

## Vérifications de charte (valeurs calculées)

| Propriété | Attendu (superx.so) | Mesuré |
|---|---|---|
| Fond de page | `#111111` | `rgb(17,17,17)` ✅ |
| Bordure de cadre | `#363636` | `rgb(54,54,54)` ✅ |
| Accent | `#ffc35b` | `rgb(255,195,91)` ✅ |
| Texte secondaire | `#a8a29e` (stone-400) | `rgb(168,162,158)` ✅ |
| Face de bouton primaire | `#2c2b2b`, rayon `11px` | `rgb(44,43,43)`, `11px` ✅ |
| H1 desktop | 60 px / 500 / `-.05em` / 1.1 | `60px` / `500` / `-3px` / `66px` ✅ |
| H1 mobile | 36 px (`text-4xl`) | `36px` / `-1.8px` / `39.6px` ✅ |

## Comportements vérifiés

- **Reduced-motion** : découpage du H1 désactivé (0 masque de mot), mot rotatif
  désactivé, lueurs orbitales à `opacity:0`, curseur custom et grain retirés,
  tout le contenu visible immédiatement.
- **Sans JS** : 0 élément à `opacity < 0.9`, H1 à `opacity: 1`, 10 135
  caractères de texte présents. Les états masqués sont conditionnés à `html.js`,
  posé par le script au démarrage — sans script, rien n'est jamais caché.
- **Tabs profils d'usage** : un seul panneau actif à la fois, rotation
  automatique, arrêt au survol et au focus, navigation aux flèches, `aria-selected`
  tenu à jour. Panneaux empilés en grille : pas de saut de hauteur à la rotation.
- **Ancres** : les 5 liens de navigation résolvent vers des sections existantes.

## Défauts trouvés et corrigés pendant la QA

| Défaut | Cause | Correction |
|---|---|---|
| Débordement horizontal de 163 px sur desktop | les halos `aurora` sortent du cadre du hero | `overflow-x: clip` sur `html` et `body` (et non `hidden`, qui aurait cassé la nav `sticky`) + halos resserrés |
| Colonne du hero à 382 px pour 358 px disponibles sur mobile | le libellé du badge était en `white-space: nowrap`, et un titre de maquette en `nowrap` imposait son `min-content` à la piste de grille | retrait du `nowrap` sur le badge, `min-width: 0` sur les enfants de grille et les titres tronqués |
| Mot rotatif du H1 invisible (un trou dans le titre) | `background-clip: text` porté par l'enveloppe ne peint pas un enfant en `position: absolute` | dégradé déplacé sur les spans `.ghost` et `.live` eux-mêmes |
| Mot rotatif rogné pendant sa transition | il était enveloppé dans un masque `overflow: hidden` du découpage de titre | le découpage saute le mot rotatif et lui applique l'animation de montée directement |
| Titre lu « Turnscientificliterature… » par les lecteurs d'écran, avec le mot rotatif doublé | découpage en spans par mot + fantôme de largeur lu deux fois | `aria-label` posé sur le H1 avant découpage, `aria-hidden` sur le fantôme et le mot animé |
| Sections bloquées à `opacity: 0` après un saut de scroll | le callback d'`IntersectionObserver` est asynchrone et fusionne les positions lors d'un saut d'ancre ou d'une restauration de scroll | remplacé par un test géométrique synchrone au scroll — tout ce qui est à hauteur de fenêtre ou déjà dépassé est révélé |
| Saut de hauteur à chaque rotation des profils d'usage | panneaux inactifs en `position: absolute` | panneaux empilés dans la même cellule de grille |
| Badge « Most popular » chevauchant le nom de l'offre | badge en absolu sans réserve d'espace | `padding-right` sur le titre de l'offre mise en avant |

## Captures

`docs/design-references/` — `desktop-hero.png`, `desktop-full.png`,
`mobile-hero.png`, `mobile-full.png`, `reduced-motion.png`, `no-js.png`.
