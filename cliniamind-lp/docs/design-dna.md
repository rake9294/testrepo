# Design DNA — superx.so

Valeurs **exactes**, extraites du bundle CSS de production
(`/_next/static/css/9c73bdd7d338d607.css`) et du HTML servi par superx.so.
Aucune valeur n'est approximée ou devinée.

> Méthode : le navigateur headless de cet environnement n'a pas d'accès réseau
> sortant, donc `getComputedStyle` sur le site live n'était pas possible. Le HTML
> et la feuille de style compilée ont été téléchargés puis lus directement — ce
> qui donne les valeurs sources littérales (encore plus fiables que le calculé).

---

## 1. Palette

### Fonds (dark, quasi-neutre, très légèrement chaud)

| Rôle | Valeur | Origine |
|---|---|---|
| Fond de page | `#111111` | `text-[#111]` / base |
| Surface 1 | `#181818` | `--tw-gradient-to:#181818` |
| Surface 2 | `#1c1c1c` | `rgb(28 28 28)` |
| Surface 3 | `#1d1d1d` | badge hero `style="background-color:#1d1d1d"` |
| Surface 4 | `#1f1f1f` | `--tw-gradient-to:#1f1f1f` |
| Surface 5 | `#222222` | `rgb(34 34 34)` |
| Surface 6 | `#262626` | `rgb(38 38 38)` |
| Surface 7 | `#2a2a2a` / `#2c2b2b` | `#2a2a2a`, face de bouton `bg-[#2C2B2B]` |
| Surface haute | `#333333` / `#363636` | `rgb(51 51 51)`, `#363636` |
| Puce sombre | `#0f0f0f` | `bg-[#0F0F0F]` (icône dans le badge) |

### Bordures

| Rôle | Valeur | Origine |
|---|---|---|
| Bordure structurelle | `#363636` | `border-[#363636]` sur `<section id="hero">` |
| Bordure douce | `#1a1a1a` | `border-b border-[#1a1a1a]` (items de menu) |
| Bordure d'icône | `#3f3f3f` | `border-2 border-[#3F3F3F]` |
| Bordure translucide | `rgba(54,54,54,.5)` | `#36363680` |

### Texte

| Rôle | Valeur | Origine |
|---|---|---|
| Primaire | `#ffffff` | `text-white` |
| Secondaire | `#a8a29e` (stone-400) | `rgb(168 162 158)` — sous-titre hero |
| Tertiaire | `#9f9f9f` / `#aaaaaa` / `#b1b1b1` | `rgb(159 159 159)`, `rgb(170 170 170)`, `rgb(177 177 177)` |
| Désactivé | `#555555` | `rgb(85 85 85)` |

### Accents (le cœur de la charte : ambre → corail)

| Rôle | Valeur | Origine |
|---|---|---|
| Accent primaire (or) | `#ffc35b` | `rgb(255 195 91)`, `text-[#FFC35B]` |
| Accent secondaire (corail) | `#fc8a65` | `rgb(252 138 101)` |
| Accent profond (orange) | `#e05c2a` | `from-[#e05c2a]` |
| Orange saturé | `#ea580c` | `rgb(234 88 12)` |
| Orange brûlé | `#c2410c` | via de gradient |
| Crème (cœur de lueur) | `#ffe4a8` | centre des `radial-gradient` de glow |
| Teinte chaude sombre | `#351d10` | `from-[#351D1045] to-[#351D10]` (fond de CTA) |
| Teinte chaude 2 | `#2f2015`, `#3d2a07` | `rgb(47 32 21)`, `rgb(61 42 7)` |

### Gradients signature

```css
/* Mot accentué du H1 */
background: linear-gradient(90deg, #fc8a65, #ffc35b); /* bg-clip-text */

/* Fond du bouton CTA primaire (enveloppe) */
background: linear-gradient(to top right, #351d1045, #351d10);

/* Badge « Most Popular » */
background: linear-gradient(90deg, rgba(224,92,42,.2), rgba(255,195,91,.2));
border + color: #ffc35b

/* Bordure du badge hero */
background: linear-gradient(135deg,#a29c9680,#52525233 20%,#52525233 80%,#a29c9680 95%);

/* Cœur des lueurs orbitales */
radial-gradient(ellipse at center,#ffe4a8 0,#ff8a5c 25%,#c45040 50%,#7a2020 75%,transparent 100%)
```

### Ombres

```css
box-shadow: 0 0 16px 4px rgba(234,88,12,.8);       /* glow fort */
box-shadow: 0 0  8px 1px rgba(234,88,12,.5);       /* glow moyen */
box-shadow: 0 0  8px     rgba(255,195,91,.4);      /* glow or */
box-shadow: inset 0 10px 40px 5px hsla(0,0%,100%,.07); /* lumière haute de carte */
box-shadow: inset 0 0 4px 4px hsla(0,0%,100%,.07);
filter:     drop-shadow(0 0 8px hsla(0,0%,100%,.31));
```

---

## 2. Typographie

- **UI / corps** : `Inter` (`--font-inter`), fallback `Inter Fallback, sans-serif`.
- **Display d'accent** : `Instrument Serif` (`--font-instrument-serif`), déclarée
  dans le bundle et réservée à des accents éditoriaux.
- **Mono** : `ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, …`.

### H1 (hero) — valeurs littérales

```
classes : text-4xl sm:text-5xl md:text-6xl font-medium tracking-tighter !leading-[1.1]
→ 2.25rem / 3rem / 3.75rem
→ font-weight 500
→ letter-spacing -0.05em
→ line-height 1.1
→ color #ffffff
```

Le dernier mot est un `<span>` en `font-semibold` (600) avec
`bg-gradient-to-r from-[#fc8a65] to-[#FFC35B] bg-clip-text text-transparent`,
monté en **mot rotatif** : un `<span class="invisible">` réserve la largeur,
un `<span class="absolute">` anime le remplacement (`transition-all duration-300 ease-in-out`).

### Sous-titre hero

```
text-base leading-relaxed  → 1rem / 1.625
color : #a8a29e (text-stone-400)
```

### Letter-spacing en usage

`-0.05em` (tracking-tighter, titres) · `-0.025em` (tracking-tight) ·
`0.025em` · `0.04em` · `0.05em` · `0.1em` (eyebrows en capitales).

---

## 3. Rayons

| Usage | Valeur |
|---|---|
| Face interne de bouton | `11px` |
| Enveloppe de bouton | `0.75rem` (12px, `rounded-xl`) |
| Cartes | `1rem` (16px), `1.5rem` (24px) |
| Divers | `5px`, `9px`, `10px`, `14px`, `20px`, `24px` |
| Pills / avatars | `9999px`, `50%` |

---

## 4. Architecture de page (signature forte)

Chaque `<section>` est un **cadre technique bordé**, pas une bande pleine largeur :

```html
<section class="relative sm:border-x border-b border-[#363636]
                mx-auto max-w-screen-2xl w-full px-4 sm:px-6 sm:w-11/12">
```

- conteneur `max-w-screen-2xl` (1536px) et `w-11/12` au-delà de `sm`
- bordures **latérales et basse** en `#363636` → l'ensemble du site se lit comme
  une grille de plan technique continue
- **marqueurs triangulaires** `#A3A3A3` (SVG 16×10, `path M0 0L8 10L16 0Z`)
  posés en `absolute top-0 -left-2` et `-right-2` sur chaque section
- **connecteurs verticaux** : SVG ligne 1px `#363636` bornée par deux cercles
  `r=5.5` remplis `#363636`
- glow de fond : image `.webp` floutée, chaude, ancrée en bas-droite du hero
  (et en bas du footer), `pointer-events:none; select-none`

### Ordre des sections observé

1. Nav
2. Hero (`Grow and monetize your 𝕏 audience, smarter/faster`)
3. Preuve sociale (avatars + note)
4. Aperçu dashboard
5. `Your Growth Dashboard, Built Into 𝕏`
6. `Discover What's Already Going Viral` (+ 3 sous-blocs H3)
7. `Create and Schedule in Minutes, Not Hours` (+ 3 H3)
8. `Engage Smarter. Grow Faster.` (+ 3 H3)
9. `Built For Serious Creators` (5 personas)
10. `One Platform. Complete Growth Infrastructure.`
11. Pricing (Pro / Advanced / Ultra, badges « Most Popular » / « Max Limits »)
12. CTA final `Ready to grow on 𝕏?`
13. Footer

---

## 5. Effets animés (CSS littéral)

### Apparition échelonnée

```css
@keyframes slide-up { 0% { opacity:0; transform:translateY(20px) } to { opacity:1; transform:none } }
.animate-slide-up { animation: slide-up .6s cubic-bezier(.22,1,.36,1) both }

@keyframes slide-up-image { 0% { opacity:0; transform:translateY(32px) } to { opacity:1; transform:none } }
.animate-slide-up-image { animation: slide-up-image .8s cubic-bezier(.22,1,.36,1) both }

@keyframes fade-in { 0% { opacity:0 } to { opacity:1 } }
.animate-fade-in { animation: fade-in 1s ease both }
```

Délais du hero, en séquence : `0ms → 80ms → 160ms → 240ms → 320ms`.
Easing maison partout : `cubic-bezier(.22, 1, .36, 1)`.

### Lueur orbitale de bouton (la signature la plus reconnaissable)

Deux blobs radiaux tournent le long du périmètre, masqués par un pseudo-élément
qui redessine la face du bouton par-dessus.

```css
.btn-border-glow-mask { position:absolute; inset:0; border-radius:inherit; overflow:hidden; z-index:0 }
.btn-border-glow-mask::after { content:""; position:absolute; inset:1.5px; border-radius:11px; background:#2c2b2b; z-index:1 }
.btn-border-glow-h,.btn-border-glow-v {
  position:absolute; border-radius:50%; filter:blur(8px);
  background:radial-gradient(ellipse at center,#ffe4a8 0,#ff8a5c 30%,#c45040 55%,transparent 80%);
}
.btn-border-glow-h { width:60px; height:35px; animation: btn-border-glow-a 3.5s ease-in-out infinite }
.btn-border-glow-v { width:35px; height:60px; animation: btn-border-glow-b 3.5s ease-in-out infinite }

@keyframes btn-border-glow-a {
  0%{left:-40px;top:-25px;opacity:0} 3%{opacity:1}
  45%{left:calc(100% - 25px);top:-25px;opacity:1}
  95%{left:calc(100% - 25px);top:calc(100% + 15px);opacity:1}
  to {left:calc(100% - 25px);top:calc(100% + 30px);opacity:0}
}
@keyframes btn-border-glow-b {
  0%{left:-25px;top:-40px;opacity:0} 3%{opacity:1}
  45%{left:-25px;top:calc(100% - 25px);opacity:1}
  95%{left:calc(100% + 15px);top:calc(100% - 25px);opacity:1}
  to {left:calc(100% + 30px);top:calc(100% - 25px);opacity:0}
}
```

Même mécanique en plus large sur la carte de pricing mise en avant
(`glow-path-a/b`, `5s`, blobs `140×80` / `80×140`, `blur(16px)`, masque
`inset:10px; border-radius:1rem; background:linear-gradient(180deg,#191919,#1f1f1f)`).

### Remplissage au survol

```css
.btn-hover-fill { position:relative; overflow:hidden }
.btn-hover-fill::before {
  content:""; position:absolute; inset:0; border-radius:inherit; z-index:0;
  background:linear-gradient(90deg,rgba(255,195,91,.12),rgba(255,150,50,.08));
  transform:scaleX(0); transform-origin:right;
  transition:transform .35s cubic-bezier(.22,1,.36,1);
}
.btn-hover-fill:hover::before { transform:scaleX(1); transform-origin:left }
```

### Balayage de lueur

```css
.btn-glow-sweep {
  position:absolute; top:-20%; left:-40%; width:45%; height:140%;
  background:radial-gradient(ellipse at center,#ffe4a8 0,#ff8a5c 25%,#c45040 45%,transparent 80%);
  filter:blur(18px); animation: btn-glow-sweep 3s ease-in-out infinite;
}
@keyframes btn-glow-sweep { 0%{left:-30%;opacity:0} 10%{opacity:1} 90%{opacity:1} to{left:110%;opacity:0} }
```

### Bordure de badge

```css
.badge-border { background: linear-gradient(135deg,#a29c9680,#52525233 20%,#52525233 80%,#a29c9680 95%) }
```
Enveloppe `p-0.5 rounded-full shadow-xl`, contenu `#1d1d1d` en `rounded-full p-1.5 pr-4`,
icône dans un rond `#0f0f0f` bordé `2px #3f3f3f`, libellé `text-sm font-light #ffffff`.

### Flou de survol

`backdrop-filter: blur(24px)` (nav) et `blur(4px)` · `filter: blur(64px)` / `blur(8px)`.

### Accessibilité

Le bundle contient un bloc `prefers-reduced-motion` qui neutralise tout :

```css
.animate-fade-in,.animate-slide-up,.animate-slide-up-image {
  animation:none!important; opacity:1!important; transform:none!important;
}
.btn-border-glow-h,.btn-border-glow-v,.pricing-glow-h,.pricing-glow-v { animation:none; opacity:0 }
.btn-hover-fill::before { transition:none }
```

---

## 6. Ce qui est repris pour ClinIAMind

| Repris tel quel | Adapté |
|---|---|
| Palette de fonds et de bordures (`#111` → `#363636`) | — |
| Accents ambre `#ffc35b` → corail `#fc8a65` | tokens isolés, échangeables en une ligne |
| Cadre technique bordé + marqueurs triangulaires | appliqué à toutes les sections |
| Lueur orbitale de bouton et de carte pricing | CTA primaire + plan « Most popular » |
| `.badge-border`, `.btn-hover-fill`, `.btn-glow-sweep` | — |
| `slide-up` échelonné 0/80/160/240/320 ms | + reveal au scroll pour le hors-écran |
| H1 `font-medium tracking-tighter leading-1.1` + mot en gradient | mot rotatif sur le vocabulaire ClinIAMind |
| Inter + Instrument Serif | serif réservé au CTA final |
| Bloc `prefers-reduced-motion` complet | étendu à tout le pack premium |
