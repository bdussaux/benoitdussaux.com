# PRD — benoitdussaux.com v2

> **Version** : 1.0
> **Auteur** : Benoît Dussaux
> **Date** : 12 mai 2026
> **Statut** : Draft → à valider avant kickoff dev
> **Cible de mise en ligne** : ASAP (v1) + itération juin 2026 (v1.1)

---

## 1. Contexte & objectifs

### 1.1 Pourquoi ce projet

Refonte du site personnel actuellement hébergé sur Webflow. Deux motivations :

1. **Réduire les coûts** : sortir de l'abonnement Webflow (~14 à 29 $/mois) vers une stack 100 % gratuite (Netlify free + domaine OVH existant).
2. **Moderniser & aligner** : créer un site qui reflète l'identité tech de Benoît (CPTO, prox developer, Claude Code user) et porte sa stratégie d'influence.

### 1.2 Stratégie portée par le site

Devenir une voix reconnue en France sur **la technologie au service des organisations à fort impact social et/ou environnemental** (associations, fondations, ESS, intérêt général).

Le site est la **carte de visite numérique** qui :
1. Convertit (LinkedIn → RDV / contact)
2. Démontre la cohérence du discours (frugalité, sobriété numérique) **par l'exécution même du site**
3. Marque le territoire de référence (SEO / GEO sur le créneau "tech + impact")

### 1.3 Anti-objectifs (ce que le site n'est PAS)

1. Pas un portfolio projets
2. Pas un blog (pour l'instant)
3. Pas une vitrine commerciale (pas de pricing, pas de services)
4. Pas un CV en ligne (LinkedIn fait ce job)

---

## 2. Personas & parcours utilisateur

### 2.1 Personas cibles

1. **Le décideur ESS** (directeur·rice d'asso, fondation, ministère) → cherche un expert tech pour un projet d'impact → veut prendre RDV vite
2. **La boîte tech mécène** (DRH, RSE, head of social impact d'une scale-up ou ESN) → cherche un interlocuteur pour structurer du mécénat de compétences tech au profit des assos → veut prendre RDV ou écrire
3. **Le pair tech** (CTO, CPO, freelance) → vérifie la crédibilité → clique LinkedIn
4. **Le journaliste / podcasteur / orga d'événement** → veut le contacter pour une intervention → cherche email + écoute le podcast
5. **Le LLM / moteur de recherche génératif** (ChatGPT, Claude, Perplexity, Google AI Overviews) → indexe pour citer Benoît sur les requêtes "tech impact social France"

### 2.2 Parcours type (30 secondes)

```
1. Arrivée → reconnaît le ton terminal → sourit
2. Lit nom + poste + manifeste court
3. Choisit 1 action : LinkedIn / RDV / Email / Podcast / GitHub
4. Quitte (ou écoute le podcast)
```

---

## 3. Spécifications fonctionnelles

### 3.1 Structure : one-pager

Une seule page HTML. Pas de routing. Pas de navigation.

### 3.2 Sections (dans l'ordre)

1. **Logo ASCII** — "BENOIT CODE" en ASCII art (réplique visuelle du logo Claude Code) avec animation au chargement (caractères qui s'écrivent un à un)
2. **Photo ronde** (border-radius 50%) — format WebP optimisé
3. **Titre H1** — `Benoît Dussaux`
4. **Sous-titre** — `J'aide les organisations à impact à tirer parti du numérique et de l'IA`
5. **Curseur clignotant** après le sous-titre (effet terminal)
6. **Manifeste court** (3-4 lignes max, ton auto-dérision douce) — voir §6
7. **Liste de liens** (style commandes terminal) :
   1. `> Accéder à mon LinkedIn` → https://www.linkedin.com/in/bdussaux/ (target=_blank, rel=noopener)
   2. `> Prendre un rendez-vous` → https://cal.com/benoit-dussaux-ekfwmd (target=_blank, rel=noopener)
   3. `> Me contacter par email` → mailto:bdussaux@gmail.com (target=_blank)
   4. `> Écouter mon passage chez Radio Contournement` → https://youtu.be/47-e8SaA76E?si=eOgcloJYHfgy_4V3 (target=_blank, rel=noopener)
   5. `> Voir mon code sur GitHub` → https://github.com/bdussaux (target=_blank, rel=noopener)
8. **Footer** :
   1. Badge `websitecarbon.com` (score live ou statique selon faisabilité — voir §5.3)
   2. Mention "Site frugal, hébergé sur Netlify, code ouvert sur GitHub"
   3. Lien vers le repo GitHub du site
   4. Année (auto-update via JS minimal ou statique)
9. **404 page** — page d'erreur custom dans le ton (ex : `404: page introuvable — même `grep -r` n'aurait rien donné`)

### 3.3 Dark mode

1. **Défaut** : mode clair (style Claude Code light)
2. **Toggle** : icône en haut à droite (☀️ / 🌙 ou caractère ASCII type `[☼]` / `[☽]`)
3. **Persistance** : `localStorage` (1 ligne JS, négligeable côté carbone)
4. **Respect** de `prefers-color-scheme` au premier chargement

---

## 4. Design — direction artistique

### 4.1 Inspiration

Claude Code en mode clair. Terminal frugal. Minimalisme radical.

### 4.2 Typographie

1. **Police unique** : JetBrains Mono (woff2, subset latin uniquement, `font-display: swap`)
2. **Hébergement** : self-hosted (pas de Google Fonts → ↓ carbone, ↑ RGPD)
3. **Hiérarchie** :
   1. Logo ASCII : taille fixe en `ch`
   2. H1 nom : ~32-40px
   3. Sous-titre : ~16-18px
   4. Corps : ~14-15px
   5. Liens / commandes : ~14-15px préfixés `>` ou `$`

### 4.3 Palette

#### Mode clair (défaut)

1. Background : `#FAFAF7` (blanc cassé chaud, type papier)
2. Texte principal : `#1A1A1A`
3. Texte secondaire : `#6B6B6B`
4. Accent / prompt : `#C96342` (orange Claude / Anthropic)
5. Lien hover : soulignement + accent

#### Mode sombre

1. Background : `#1A1A1A`
2. Texte principal : `#E8E6E1`
3. Texte secondaire : `#8B8B8B`
4. Accent / prompt : `#D97757`

### 4.4 Animations

1. **Logo ASCII** : animation caractère par caractère au chargement (~600-800ms total, fonction `requestAnimationFrame`, fallback statique si `prefers-reduced-motion`)
2. **Curseur clignotant** : `@keyframes blink` CSS pur (1s, infinite)
3. **Pas d'autres animations** (pas de scroll-jacking, parallax, transitions lourdes)

### 4.5 Layout

1. **Centré**, max-width ~640px
2. **Padding généreux**, beaucoup d'air
3. **Pas de grille bento**, pas de cards, pas de borders décoratives
4. **Mobile-first**, scaling fluide via `clamp()`

### 4.6 Photo

1. Format : WebP, qualité 75-80, dimensions max 320×320 px (servie en 160×160 affichage)
2. `<img>` avec `loading="lazy"` (ou `eager` si above-the-fold — à trancher), `width` et `height` explicites
3. `alt` descriptif : `Photo de Benoît Dussaux, souriant.`
4. Cadre : border-radius 50% pur CSS, pas de masque SVG

---

## 5. Empreinte carbone — règles strictes

### 5.1 Objectifs chiffrés

1. **Score WebsiteCarbon** : viser **A+** (< 0.10 g CO₂e / visite)
2. **Poids total page (HTML + CSS + JS + image + font)** : viser **< 100 Ko**
3. **Requêtes HTTP** : viser **< 10** au total
4. **Lighthouse Performance** : 100/100
5. **Lighthouse Accessibility** : 100/100
6. **Lighthouse SEO** : 100/100
7. **Lighthouse Best Practices** : 100/100

### 5.2 Règles de sobriété appliquées

1. **Aucun framework JS** (pas de React, Vue, Astro, Eleventy)
2. **HTML statique** servi tel quel
3. **CSS inline** dans `<style>` (pas de fichier externe → -1 requête)
4. **JS minimal inline** : uniquement pour (a) animation ASCII, (b) toggle dark mode, (c) curseur clignotant peut être en CSS pur
5. **Pas de tracking, pas d'analytics, pas de cookies**
6. **Pas de CDN tiers** (fonts self-hosted, pas de Google Fonts, pas de jQuery, pas d'icônes externes)
7. **Pas d'iframe** (pas d'embed Spotify, YouTube, Calendly)
8. **Compression** : Brotli activé via Netlify (par défaut)
9. **Cache headers** longs pour assets (font, image) via `netlify.toml`
10. **Photo** : 1 seule image, format WebP, dimensions strictes
11. **Favicon** : SVG inline ou émoji en base64 (1 caractère)
12. **Pas de service worker** ni PWA (pas nécessaire pour un one-pager)

### 5.3 Affichage du score carbone

1. **Option A (préférée)** : badge statique avec score mesuré, mis à jour manuellement à chaque deploy majeur (zéro requête tierce)
2. **Option B** : lien `target="_blank"` vers la page de test WebsiteCarbon du site (zéro requête, juste un lien)
3. **À éviter** : badge dynamique fetch en JS (génère une requête)

→ **Recommandation : Option A**

---

## 6. Ton & contenu

### 6.1 Tone of voice

1. **Auto-dérision douce** : on se moque gentiment du milieu tech, des buzzwords, de soi-même
2. **Sec & efficace** : phrases courtes, pas d'adverbes mous
3. **Geek assumé** : références terminal, mais accessibles
4. **Sérieux sur le fond** (impact, ESS) — léger sur la forme

### 6.2 Proposition de manifeste (à valider/réécrire)

> Je mets la tech au service des organisations à impact.
> Sans buzzword et sans IA générative qui résout les inégalités dans le monde en un prompt.
> Juste des outils qui marchent, pour des gens qui font.

### 6.3 Page 404 (proposition)

```
$ find / -name "cette-page"
find: aucun résultat.

Soit elle n'existe pas, soit elle a été supprimée
dans un grand ménage de printemps.

> Retour à l'accueil
```

### 6.4 Microcopy des liens

Format proposé (à valider) :

```
$ open linkedin       # Accéder à mon LinkedIn
$ book meeting        # Prendre un rendez-vous
$ send email          # Me contacter par email
$ play podcast        # Mon passage chez Radio Contournement
$ git clone bdussaux  # Voir mon code sur GitHub
```

---

## 7. SEO & GEO

### 7.1 Mots-clés cibles (5 prioritaires)

1. Tech pour associations
2. Numérique impact social
3. Transformation digitale ESS
4. IA pour le secteur associatif
5. Directeur produit fondation / venture philanthropy

### 7.2 Balises HTML SEO

1. `<title>` : `Benoît Dussaux — La tech pour les organisations à impact`
2. `<meta name="description">` : ~150 caractères, intégrant 2-3 mots-clés
3. `<meta name="author">` : `Benoît Dussaux`
4. `<link rel="canonical">` vers https://benoitdussaux.com
5. `lang="fr"` sur `<html>`

### 7.3 Open Graph & Twitter Cards

1. `og:title`, `og:description`, `og:url`, `og:type=website`
2. `og:image` : SVG (ou WebP) sobre, 1200×630 px, texte "Benoît Dussaux — CPTO" sur fond crème, style terminal
3. `twitter:card=summary_large_image`

### 7.4 JSON-LD Schema.org

Bloc `<script type="application/ld+json">` avec type `Person` :

```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Benoît Dussaux",
  "jobTitle": "Chief Product & Technology Officer",
  "worksFor": { "@type": "Organization", "name": "Fondation AlphaOmega" },
  "url": "https://benoitdussaux.com",
  "image": "https://benoitdussaux.com/photo.webp",
  "sameAs": [
    "https://www.linkedin.com/in/bdussaux/",
    "https://github.com/bdussaux"
  ],
  "address": { "@type": "PostalAddress", "addressLocality": "Paris", "addressCountry": "FR" },
  "knowsAbout": [
    "Product Management",
    "Transformation digitale",
    "Économie sociale et solidaire",
    "Intelligence artificielle pour associations",
    "No-code"
  ]
}
```

### 7.5 GEO (Generative Engine Optimization)

1. **`llms.txt`** à la racine, format Markdown, ~30-50 lignes, structuré :
   - Qui je suis (1 paragraphe)
   - Mon expertise (liste)
   - Mon parcours (timeline courte)
   - Comment me contacter
   - Sujets sur lesquels me citer
2. **`/llms-full.txt`** (optionnel v1.1) : version longue avec citations possibles
3. **Contenu HTML riche en facts citables** : phrases courtes, factuelles, autonomes (les LLM extraient mieux)
4. **`robots.txt`** : autoriser tous les bots y compris GPTBot, ClaudeBot, PerplexityBot, Google-Extended

### 7.6 Sitemap

`sitemap.xml` minimal (1 URL, c'est un one-pager) à la racine.

---

## 8. Accessibilité & qualité (Opquast)

### 8.1 Règles Opquast prioritaires à respecter

1. **Contraste** : tous les textes ≥ AAA WCAG (mode clair ET sombre)
2. **Navigation clavier** : tous les liens focusables, ordre logique, focus visible
3. **`prefers-reduced-motion`** : désactive animation ASCII et curseur clignotant
4. **`lang="fr"`** déclaré
5. **`alt`** sur la photo, descriptif et non décoratif
6. **`target="_blank"`** toujours assorti de `rel="noopener noreferrer"`
7. **Liens externes** : icône ↗ ou texte indiquant qu'ils ouvrent un nouvel onglet
8. **Pas de `<div>` cliquable** — uniquement des `<a>` ou `<button>`
9. **Structure sémantique** : `<header>`, `<main>`, `<footer>`, `<h1>` unique
10. **Meta viewport** correctement définie
11. **Favicon** présent
12. **HTTPS** forcé (Netlify le fait par défaut)
13. **Page 404** custom
14. **Pas de surveillance ni cookies tiers** → conforme RGPD sans bandeau
15. **Temps de chargement < 1s** sur 3G simulée

---

## 9. Stack technique

### 9.1 Stack retenue

1. **Front** : HTML5 + CSS inline + JS minimal inline, écrits à la main
2. **Pas de build** : push sur `main` → déploiement direct Netlify
3. **Versioning** : GitHub, repo public `bdussaux/benoitdussaux.com`
4. **Hébergement** : Netlify free tier
5. **DNS** : OVH, domaine `benoitdussaux.com` pointant vers Netlify (CNAME ou ALIAS)
6. **Email** : mailto direct, pas de form

### 9.2 Structure du repo

```
benoitdussaux.com/
├── index.html
├── 404.html
├── photo.webp
├── og.webp (ou og.svg)
├── favicon.svg
├── robots.txt
├── sitemap.xml
├── llms.txt
├── netlify.toml
├── README.md
└── docs/
    └── PRD.md
```

### 9.3 `netlify.toml` (config clé)

1. Build command : aucune
2. Publish directory : `.` (racine)
3. Headers :
   1. `Cache-Control: public, max-age=31536000, immutable` sur fonts et images
   2. `Cache-Control: public, max-age=3600` sur HTML
   3. CSP strict (auto-hébergement, aucun tiers)
   4. `X-Content-Type-Options: nosniff`
   5. `Referrer-Policy: strict-origin-when-cross-origin`
4. Redirects : `/404` → 404.html (déjà géré par défaut)

### 9.4 Workflow déploiement

1. Edit local (VSCode / Cursor)
2. `git commit && git push origin main`
3. Netlify détecte push → déploie en ~10s
4. Preview deploy sur PR (optionnel)

---

## 10. Roadmap

### 10.1 v1 — ASAP (mai 2026)

1. Wireframe basse-fi (1 image / Excalidraw)
2. Maquette HTML statique (1 fichier, mode clair uniquement d'abord)
3. Logo ASCII finalisé (choix entre statique stylé ou animé)
4. Photo optimisée
5. SEO + JSON-LD + OG image
6. Repo GitHub créé, push initial
7. Connexion DNS OVH → Netlify
8. Tests : Lighthouse, WebsiteCarbon, Opquast checklist
9. Récupération du score WebsiteCarbon → injection statique dans le footer
10. Mise en ligne sur benoitdussaux.com

### 10.2 v1.1 — Itération juin 2026

1. Dark mode + toggle
2. Page 404 custom
3. `llms.txt` enrichi
4. Animation ASCII si pas faite en v1
5. Affinage du ton (manifeste, microcopy) après feedback réel

### 10.3 v2 — futur (TBD)

1. Ajout section "Articles & prises de parole" quand le contenu sera prêt
2. Version EN (optionnelle)

---

## 11. Critères d'acceptation (Definition of Done v1)

1. ✅ Site accessible sur https://benoitdussaux.com
2. ✅ Score WebsiteCarbon ≥ A+ (< 0.10 g CO₂e)
3. ✅ Lighthouse 100/100/100/100
4. ✅ Poids total page < 100 Ko
5. ✅ Tous les liens fonctionnels, target=_blank + rel=noopener où requis
6. ✅ Photo affichée en cercle parfait
7. ✅ Logo ASCII "BENOIT CODE" présent et lisible
8. ✅ JSON-LD Person valide (testé via validator.schema.org)
9. ✅ `robots.txt`, `sitemap.xml`, `llms.txt` présents
10. ✅ HTTPS forcé, HSTS activé
11. ✅ Test sur mobile (Safari iOS) et desktop (Chrome, Firefox)
12. ✅ Repo GitHub public, README rempli
13. ✅ Au moins 1 commande terminal interactive ? → **NON, hors scope** (pas d'easter egg en v1 selon décision)

---

## 12. Points ouverts à trancher

1. **Logo ASCII** : choix entre (a) statique stylé type bannière, (b) animé caractère par caractère, (c) cyclique entre plusieurs frames ASCII. → **Reco : animation au chargement uniquement, puis statique.**
2. **Manifeste** : valider la version proposée en §6.2 ou réécrire ensemble.
3. **OG image** : la générer en SVG (ultra-light) ou WebP (plus universel) ?
4. **Curseur clignotant** : après le sous-titre uniquement, ou aussi sur la ligne de prompt des liens ?
5. **Affichage du score carbone** : Option A (badge statique) confirmée ?
6. **Email** : Garder `bdussaux@gmail.com` ou créer une adresse pro type `hello@benoitdussaux.com` ?
