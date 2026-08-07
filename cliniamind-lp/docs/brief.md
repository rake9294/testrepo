# Brief — refonte LP ClinIAMind

## Demande

Proposer une nouvelle version de la landing page de **cliniamind.com**, en
brouillon, en **récupérant le contenu existant** et en **s'inspirant de
superx.so pour la charte graphique et le design**.

## Cadre

| | |
|---|---|
| Produit | ClinIAMind — plateforme d'intelligence documentaire scientifique pour la santé régulée |
| Cible | Consultants, PME, équipes Affaires Réglementaires |
| Promesse (inchangée) | Turn scientific literature into traceable, audit-ready evidence |
| Langue du contenu | Anglais — celle du site source, conservée |
| Stack | HTML autonome, fichier unique, aucune dépendance ni build |
| Statut | Brouillon → `noindex` + `robots.txt` de blocage |
| Référence design | superx.so |

## Sources

- **Contenu** : `https://cliniamind.com` — HTML servi + charge utile i18n
  intégrée (les réponses de la FAQ et les 3 profils d'usage complets n'étaient
  pas dans le DOM rendu, ils ont été récupérés depuis cette charge).
- **Design** : `https://superx.so` — HTML + bundle CSS de production
  (`/_next/static/css/9c73bdd7d338d607.css`), valeurs littérales relevées dans
  `design-dna.md`.

> Le navigateur sans interface de cet environnement n'a pas d'accès réseau
> sortant : l'extraction par `getComputedStyle` sur le site live n'était pas
> possible. Lire la feuille de style compilée donne les valeurs sources
> elles-mêmes, ce qui est au moins aussi fiable. Chromium a en revanche servi
> pour la QA de la page produite, en local.

---

## Direction retenue

**Dark premium chaud, structure en plan technique.**

Reprise fidèle de la charte superx.so, parce que c'est ce qui a été demandé, et
parce que ses deux partis pris les plus forts servent bien ClinIAMind :

1. **Le cadre bordé continu** (`border-x` + `border-b` en `#363636`, marqueurs
   triangulaires aux angles) fait lire la page comme un document technique
   structuré. Pour un produit qui vend de la traçabilité et de l'auditabilité,
   c'est cohérent avec la promesse plutôt que décoratif.
2. **La lueur orbitale ambre** sur le CTA et l'offre mise en avant apporte le
   côté « agence » sans jamais recourir à une couleur criarde à plat.

Le sombre neutre `#111`–`#222` met aussi mieux en valeur la maquette produit du
hero, qui est l'élément le plus convaincant de la page.

### Alternative — même système, accent froid

L'ambre est chaud et un peu « growth / créateur ». Le site actuel de ClinIAMind
utilise des dégradés bleu-cyan-émeraude, plus proches des codes du médical
régulé. Toute la structure, la mise en page et les effets restent identiques :
seules trois variables changent en tête de `index.html`.

```css
/* Variante froide, alignée sur la charte ClinIAMind actuelle */
--accent:#4fc08d;      /* au lieu de #ffc35b */
--accent-2:#38bdf8;    /* au lieu de #fc8a65 */
--accent-3:#0ea5e9;    /* au lieu de #e05c2a */
```

Les lueurs (`--accent-cream`, `--warm-1`) et les fonds teintés
`rgba(255,195,91,…)` demanderaient un passage rapide pour être ré-accordés.
Un mot suffit pour que je produise la variante complète.

---

## Correspondance contenu → sections

| Section de la page | Origine |
|---|---|
| Nav (Benefits, Evidence, Product flow, Testimonials, Pricing) | identique |
| Badge hero | `AI-powered literature intelligence for regulated healthcare teams` |
| H1 | `Turn scientific literature into traceable, audit-ready evidence` |
| Sous-titre, CTA, preuve sociale | mot pour mot |
| Maquette produit | reprise de la démo du site (IVDR Project 2024, 234 publications, résumé IA 97,3 % / 99,1 % / n=1 248 / niveau 1b, rapport SVR 156 pages) |
| Bandeau de valeur (4 items) | les 4 libellés de compteurs du site — **sans les chiffres**, voir plus bas |
| Marquee | les puces de fonctionnalités listées sur le site |
| 4 blocs produit | Smart library / Semantic search / AI annotations / Export & documentation, titres, textes et puces à l'identique |
| How it works | les 3 étapes, textes intégraux |
| Témoignages | les 3 citations, rôles, secteurs et accroches, mot pour mot |
| Profils d'usage | Consultants / SMEs & Companies / Regulatory Affairs, avec les 5 « key features » de chacun |
| Bénéfices | les 4, titres et descriptions |
| Tarifs | Free 0 € / Starter 49 € / Professional 149 € / Enterprise 399 €, toutes les puces et la mention TVA |
| FAQ | les 6 questions **avec leurs réponses** |
| CTA final | badge, double titre, description, 4 réassurances |
| Pied de page | 3 colonnes, certifications, copyright, mention d'hébergement |

Aucun texte n'a été inventé ni réécrit. Un seul ajout rédactionnel : le titre de
la section bénéfices, `Why teams switch to ClinIAMind` — le site n'en a pas, la
section y arrive sans intertitre.

---

## Points ouverts

### 1. Les quatre chiffres du bandeau — à fournir

Le site affiche quatre compteurs animés qui démarrent à `0` :
`0%` *Less time spent on literature review* · `0+` *PDFs analyzed per project* ·
`0%` *Full audit traceability* · `0/7` *Always available*.

Les valeurs cibles ne sont ni dans le HTML servi, ni dans la charge i18n, ni
dans les fragments JavaScript téléchargeables — elles vivent dans un composant
chargé à la demande. **Je ne les ai donc pas inventées** : le bandeau reprend
les quatre libellés sous forme de puces, sans nombre. Donne-moi les quatre
valeurs et je remets le compteur animé.

### 2. Le mot rotatif du H1

Signature reprise de superx.so (`smarter` → `faster`). Ici :
`audit-ready` → `traceable` → `defensible` → `reusable`.
`audit-ready` vient du site ; les trois autres sont du vocabulaire déjà présent
ailleurs dans la page (`traceable`, `defensible for notified body review`,
`reusable outputs`), mais c'est de l'écriture, pas de la reprise. À valider ou
à réduire au seul mot d'origine — un attribut `data-rotate` à éditer.

### 3. Liens

Les liens pointent vers les chemins du site actuel (`/sign-up`, `/sign-in`,
`/contact`, `/privacy`…). À vérifier avant toute mise en ligne.

### 4. Avatars de preuve sociale

Le site affiche cinq pastilles `DR TM SL AB CM` sans photo. Reprises telles
quelles, en initiales — donc aucune identité inventée.
