# Portfolio · Olivier Vernet — TP2 Animation CSS & JavaScript

Mini-portfolio personnel statique HTML/CSS/JS — deuxième TP du programme **TIM** (Technique d'intégration multimédia, Collège de Maisonneuve).

**Démo live :** https://netoli.github.io/s2-2w2-TP1/

---

## Le projet

Site personnel d'une page divisée en 4 sections (POrTFOLIO/Bienvenue, Moi, Formations, Réalisations). L'objectif pédagogique du TP était la **maîtrise des animations CSS** (`@keyframes`, `transform`, `clip-path`, `transition`) et la **manipulation de l'état** sans framework (checkbox-hack, radios CSS-only, scroll-triggered fade-in en JS minimal).

### Techniques mises en pratique
- **16 animations `@keyframes`** : effet 3D lettre-par-lettre sur les titres, défilement, rotation, transparence, mutation de `clip-path`, déplacement vertical/horizontal des formes d'arrière-plan.
- **Burger menu CSS-only** via checkbox-hack + scroll-lock JS.
- **Accordéon Moi** — bascule "Voir plus" via `<input type="checkbox">` + sélecteur `~`.
- **Onglets Formations** — 4 radios pilotent l'affichage de la description correspondante (CSS-only, pattern tablist).
- **80 formes décoratives** en arrière-plan (carrés/cercles/triangles/trapèzes) avec animations imbriquées et `animation-delay` staggered.
- **Picture sources responsive** (`<picture>` + `<source media>` à 576px et 992px).
- **Scroll-triggered fade-in** en JavaScript vanilla : `getBoundingClientRect()` + opacity/translate sur les `.forme`.

## Refonte portfolio (avril 2026)

La version livrée en classe a été polish pour devenir une pièce de portfolio publiable.

### Sémantique & accessibilité
- Skip-link « Aller au contenu principal ».
- Hiérarchie de titres rétablie : ~16 `<h2>`/`<h3>` détournés (textes de paragraphe, coordonnées, descriptions de cours) remplacés par `<p>` ou éléments de liste.
- `<h2 visually-hidden>` ajoutés à chaque section pour donner un nom accessible (`aria-labelledby`).
- **Bug HTML invalide corrigé** : `<ul><a><li>...</li></a></ul>` (interdit par la spec) → `<ul><li><a>...</a></li></ul>`.
- Toutes les icônes Material `aria-hidden="true"` (purement décoratives — le texte adjacent porte l'info).
- 4 `<h2 class="coordonnees">` détournés en haut + 4 en bas → `<ul>` avec `<li>` et liens cliquables (`tel:`, `mailto:`, GitHub, LinkedIn).
- Burger menu : `aria-label`, `role="button"`, `tabindex="0"`.
- Onglets formations : `role="tablist"` / `role="tab"` / `role="tabpanel"`.
- Animation 80-formes : `aria-hidden="true"` sur le conteneur (purement décorative).
- Bouton « retour en haut » : `aria-label` (avant c'était juste l'icône Material vide pour les AT).
- Formulaire infolettre : `for="email"` cassé → `for="courriel"` correct, `<form>` réel, `autocomplete="email"`, `required`.
- Alt descriptifs sur photo de profil, images décoratives en `alt=""` + `aria-hidden`.
- Liens externes : `target="_blank" rel="noopener noreferrer"`.

### SEO
- Title contextualisé ("TP1" → "Portfolio · Olivier Vernet — Intégrateur multimédia").
- `meta description`, `meta author`, `meta theme-color`.
- Open Graph (type/title/description/url), Twitter card `summary_large_image`.
- `<link rel="canonical">`.

### Performance
- `<link rel="preconnect">` vers `fonts.googleapis.com` + `fonts.gstatic.com`.
- `loading="lazy"` sur les images sous le pli, `loading="eager"` explicite sur le LCP.
- `prefers-reduced-motion` supporté : toutes les animations désactivées pour utilisateurs sensibles aux mouvements.

### Polish CSS
- 4 keyframes de mouvement vertical (`deplacement-vertical-ligne[12](triangle|trapeze)`) **réécrites** : ajout d'oscillation horizontale subtile (`translateX` ±2vw) et rotation 360° pendant le trajet — mouvement plus organique au lieu d'une chute droite.
- `:focus-visible` global (outline doré 3px) sur tous les éléments focusables.
- Sélecteurs CSS ajustés suite aux changements HTML (`.rsociaux > li > a > img`, `.reprise-menu > ul > li > a`, etc.).
- Hover transitions adoucies (200ms ease).

### Typos corrigées
- "Oivier" → "Olivier"
- "parcous" → "parcours"
- "annéee" → "année"
- "Technique d'intégration multimédias" → "multimédia"

---

## Stack

- **HTML5** sémantique
- **CSS3** : `@keyframes`, `clip-path`, `transform` 3D, `<picture>`/`<source>`, custom timing-functions
- **JavaScript vanilla** : event listeners, `getBoundingClientRect`, manipulation DOM minimale
- **Aucun framework, aucune dépendance externe** (sauf Google Fonts + Material Icons)

## Structure

```
s2-2w2-TP1/
├── index.html
├── README.md
└── assets/
    ├── css/
    │   └── index.css   # ~1500 lignes — design + 16 keyframes + responsive + a11y utilities
    ├── js/
    │   └── index.js    # 80 lignes — burger scroll-lock + scroll-trigger fade-in
    └── images/
        ├── header-main/
        └── footer/
```

## Apprentissages

- **CSS-only state management** : le checkbox-hack + sélecteurs `~` permettent de remplacer beaucoup de JS avec une logique 100 % déclarative. Pratique pour les TP, mais limites a11y (pas de `aria-expanded` qui change dynamiquement) — à upgrader avec un peu de JS sur projet réel.
- **Animations stackées** : combiner 4 keyframes simultanées (`changement-taille`, `changement-couleur`, `modification-forme-*`, `deplacement-*`) avec des durées et délais différents donne un effet riche sans surcharge perçue.
- **Sémantique vs visuel** : la version originale empilait `<h2>` et `<h3>` partout pour leur **style**, pas leur **rôle**. Refondre avec des `<p>` + classes utility a forcé une vraie réflexion : est-ce un titre de section, ou juste du texte stylé ?
- **`prefers-reduced-motion` n'est pas optionnel** quand on construit un fond animé permanent — c'est le minimum vital pour l'inclusivité.

## Auteur

**Olivier Vernet** — étudiant TIM, Collège de Maisonneuve · [GitHub @netoli](https://github.com/netoli)
