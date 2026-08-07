# ClinIAMind — Landing page (draft)

Nouvelle version de la landing page de **cliniamind.com**, avec le **contenu
existant repris intégralement** et une **charte graphique inspirée de
[superx.so](https://superx.so)**.

Construite avec la méthode du plugin `premium-lp-studio` fourni (extraction de
Design DNA → direction → build avec le pack premium → QA).

## Ouvrir la page

```bash
# fichier unique, aucune dépendance ni build
open cliniamind-lp/index.html

# ou via un petit serveur, pour tester les ancres proprement
python3 -m http.server 8080 --directory cliniamind-lp
```

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `index.html` | La landing page complète — HTML + CSS + JS en un seul fichier |
| `robots.txt` | Blocage d'indexation (c'est un brouillon) |
| `docs/design-dna.md` | Charte de superx.so, valeurs exactes extraites du bundle de prod |
| `docs/brief.md` | Brief, direction retenue, correspondance contenu, points ouverts |
| `docs/qa-report.md` | Résultats des tests (4 scénarios) |
| `docs/design-references/` | Captures desktop, mobile, reduced-motion, sans JS |

## Ce qui vient de superx.so

- Palette sombre neutre `#111` → `#363636` et accents ambre `#ffc35b` → corail `#fc8a65`
- Le **cadre technique bordé** avec marqueurs triangulaires autour de chaque section
- La **lueur orbitale** qui tourne le long du CTA primaire et de la carte « Most popular »
- Le badge à bordure dégradée, le remplissage de bouton au survol
- H1 `font-weight:500 / tracking -.05em / line-height 1.1` avec un mot en dégradé, rotatif
- Apparitions échelonnées 0/80/160/240/320 ms, easing `cubic-bezier(.22,1,.36,1)`

Toutes les valeurs sont sourcées dans `docs/design-dna.md`.

## Ce qui vient de cliniamind.com

Tout le texte : hero, 4 blocs produit, les 3 étapes, les 3 témoignages, les 3
profils d'usage, les 4 bénéfices, les 4 offres tarifaires, les 6 questions de la
FAQ, le CTA final et le pied de page — repris **mot pour mot**, sans réécriture.

## Changer la teinte d'accent

Toute la couleur passe par trois variables au début de `index.html` :

```css
--accent:#ffc35b;    /* or     */
--accent-2:#fc8a65;  /* corail */
--accent-3:#e05c2a;  /* orange */
```

Les remplacer re-teinte l'ensemble du site (boutons, lueurs, badges, dégradés de
titre, icônes, barres de progression). Voir `docs/brief.md` pour la variante
cyan/teal, plus proche de la charte actuelle de ClinIAMind.

## Accessibilité et robustesse

- `prefers-reduced-motion` : toutes les animations coupées, contenu entièrement visible
- Sans JavaScript : aucun contenu masqué (les états cachés sont conditionnés à `html.js`)
- Titres, `aria-label` sur le H1 découpé, tabs au clavier (flèches), focus visibles
- Zéro requête réseau hors la police Google Fonts (fallbacks système en place)
