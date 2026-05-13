# PRD — benoitdussaux.com v2

> **Version** : 1.3
> **Auteur** : Benoît Dussaux
> **Date** : 13 mai 2026
> **Statut** : Validé — implémenté dans le prototype HTML, prêt pour finalisation des assets et déploiement
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

1. **En-tête** : Logo ASCII massif "BENOIT CODE" (style figlet `ansi_shadow`, proche du logo Claude Code) en pleine largeur — sert également de `<h1>` sémantique avec `aria-label="Benoît Dussaux"`
2. **Phrase d'introduction** (narrative + factuelle, porte le naming + le positionnement SEO) :
   > On m'a dit que mon métier allait être remplacé par Claude Code. J'ai donc forké et lancé **Benoit Code** — une CLI pour une tech simple, utile et efficace pour les organisations à impact.
3. **Curseur clignotant** après l'intro (effet terminal)
4. **Manifeste** (3 paragraphes, voir §6)
5. **CLI interactive** (remplace la liste de liens classique) :
   1. Titre `$ benoit --help`
   2. Zone d'output dynamique au-dessus de la box (lignes "fake exécution" en gris dim)
   3. Box prompt avec caret `›` orange + champ `<input>` libre, fond `--bg-alt`
   4. Hint : "↵ pour exécuter · ↑↓ pour l'historique · `help` pour la liste"
   5. Chips de suggestions cliquables sous la box : `linkedin`, `rdv`, `email`, `podcast`, `github`, `help`
   6. Comportement au clic d'un chip : remplit la box ET lance la commande
   7. Comportement à la saisie + ↵ : exécute la commande
   8. Comportement par commande :
      - 3 lignes de "fausse exécution" en français, espacées de ~350ms
      - Après 1.5s, redirection vers l'URL cible (`_blank` sauf `mailto:`)
      - Pendant l'exécution : box et chips désactivés (visuel `opacity: 0.65`)
   9. Commande inconnue : message d'erreur en français + invitation à cliquer sur les suggestions
   10. **Historique du terminal persistant pendant la session** : les commandes successives s'empilent dans l'output (vrai comportement terminal), une ligne vide aère après chaque commande. Au rechargement de la page : reset complet (rien en localStorage)
   11. **Auto-scroll** vers la box d'input à chaque nouvelle ligne (`scrollIntoView` smooth)
   12. **Historique des commandes** navigable avec ↑↓ pour rappeler les commandes précédemment tapées

   **Fake-exécutions finalisées par commande** :

   - `linkedin` → LinkedIn (`_blank`)
     1. `auth OK · profil chargé...`
     2. `chargement de mon LinkedIn officiel (oui, c'est bien ça)...`
     3. `redirection en cours vers LinkedIn...`

   - `rdv` → cal.com (`_blank`)
     1. `parsing du calendrier...`
     2. `exclusion des créneaux avant 9h30 (le café d'abord)...`
     3. `redirection vers cal.com...`

   - `email` → mailto (`_self`)
     1. `préparation du brouillon...`
     2. `(je réponds sous 48h ouvrées en général)`
     3. `ouverture de votre client mail...`

   - `podcast` → YouTube Radio Contournement (`_blank`)
     1. `chargement de l'épisode #73 de Radio Contournement...`
     2. `enregistré en 2021, mes opinions n'ont pas trop bougé...`
     3. `lancement de la lecture...`

   - `github` → GitHub (`_blank`)
     1. `ouverture du repo...`
     2. `disclaimer : peu de code, beaucoup d'ambitions...`
     3. `redirection vers GitHub...`

   - `help` → pas de redirection, liste les commandes disponibles avec une astuce finale
6. **Widget WhatsApp flottant** (`position: fixed`, bas-droite) :
   1. Photo ronde 80×80 (55×55 en mobile) au centre
   2. Texte rotatif `· ping benoit · TOUJOURS UP · ping benoit · TOUJOURS UP ·` autour de la photo (SVG `textPath`, animation CSS 20s linear infinite)
   3. Rayon réduit (52 sur viewBox 140) pour rapprocher le texte de la photo
   4. Lien vers WhatsApp : `https://wa.me/33640141733` (sans message pré-rempli, target=_blank)
   5. Désactivation de la rotation si `prefers-reduced-motion: reduce`
   6. Mobile : widget réduit (100×100 conteneur, 55×55 photo)
   7. Hover : zoom doux de la photo (+8%)
7. **Footer** :
   1. Badge `websitecarbon.com` (score statique mis à jour manuellement)
   2. Mention "Site frugal, hébergé sur Netlify, code ouvert sur GitHub"
   3. Lien vers le repo GitHub du site
   4. Année (auto-update via JS minimal)
8. **404 page** — page d'erreur custom dans le ton (à venir en v1.1)

**Note SEO** : pas de `<h1>` textuel séparé (évite le doublon avec le logo). Le `<h1>` est porté par le bloc logo ASCII via `aria-label`, ce qui préserve la sémantique et le référencement. Les liens "officiels" (LinkedIn, GitHub, etc.) restent crawlables car ils sont déclarés dans le JS de la CLI ; le JSON-LD `sameAs` couvre l'essentiel pour le SEO.

### 3.3 Dark mode

1. **Défaut** : mode **sombre** (style Claude Code dark, choix assumé)
2. **Toggle** : icône en haut à droite (`[ ☽ ]` / `[ ☼ ]`)
3. **Persistance** : `localStorage` (clé `theme`, valeurs `light` ou `dark`)
4. **Pas de respect automatique de `prefers-color-scheme`** : le dark mode est imposé par défaut pour matcher l'identité Claude Code. Si l'utilisateur préfère clair, il clique le toggle (la préférence est mémorisée).
5. **`meta name="color-scheme"`** déclare `dark light`
6. **`meta name="theme-color"`** mis à jour dynamiquement par le JS pour synchroniser la barre d'adresse mobile

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

#### Mode sombre (défaut)

1. Background : `#1A1A1A`
2. Background alt (CLI box) : `#232323`
3. Texte principal : `#E8E6E1`
4. Texte secondaire : `#8B8B8B`
5. Accent / prompt : `#D97757` (orange Claude / Anthropic)
6. Border : `#2E2E2E`
7. Error : `#C97171`

#### Mode clair

1. Background : `#FAFAF7` (blanc cassé chaud, type papier)
2. Background alt (CLI box) : `#F0EFE9`
3. Texte principal : `#1A1A1A`
4. Texte secondaire : `#6B6B6B`
5. Accent / prompt : `#C96342`
6. Border : `#E5E3DC`
7. Error : `#B5322F`

### 4.4 Animations

1. **Curseur clignotant** après l'intro : `@keyframes blink` CSS pur (1s, infinite)
2. **Widget WhatsApp** : rotation continue du texte autour de la photo, `@keyframes spin` 20s linear infinite
3. **CLI fake exécution** : 3 lignes en français qui s'affichent toutes les ~350ms, puis redirection après 1.5s
4. **Hover photo WhatsApp** : zoom 8% + transition douce (0.2s)
5. **Toutes les animations** désactivées si `prefers-reduced-motion: reduce`

### 4.5 Layout

1. **Centré**, max-width ~720px
2. **En-tête** : logo ASCII en pleine largeur, sans photo (la photo passe en widget WhatsApp flottant)
3. **Padding généreux**, beaucoup d'air
4. **Pas de grille bento**, pas de cards, pas de borders décoratives
5. **Mobile-first**, scaling fluide via `clamp()`
6. **Logo ASCII** : taille adaptée à la largeur du container, scroll horizontal en dernier recours sur mobile très étroit
7. **Widget WhatsApp** : `position: fixed`, bas-droite, hors du flux normal de la page

### 4.6 Photo

1. Format : WebP, qualité 75-80, dimensions source 160×160 px (servie en 80×80 affichage, 55×55 sur mobile, prise en compte rétina)
2. `<img>` avec `loading="eager"` (above-the-fold dans le widget WhatsApp), `width` et `height` explicites
3. `alt` descriptif : `Photo de Benoît Dussaux`
4. Cadre : border-radius 50% pur CSS, centrée dans le widget WhatsApp

---

## 5. Empreinte carbone — règles strictes

### 5.1 Objectifs chiffrés

1. **Score WebsiteCarbon** : viser **A+** (< 0.10 g CO₂e / visite)
2. **Poids total page (HTML + CSS + JS + image + font)** : viser **< 100 Ko** (estimé ~50-60 Ko en prod : ~20 Ko HTML, ~15 Ko photo WebP, ~25 Ko font woff2 subset)
3. **Requêtes HTTP** : viser **< 10** au total
4. **Lighthouse Performance** : 100/100
5. **Lighthouse Accessibility** : 100/100
6. **Lighthouse SEO** : 100/100
7. **Lighthouse Best Practices** : 100/100

### 5.2 Règles de sobriété appliquées

1. **Aucun framework JS** (pas de React, Vue, Astro, Eleventy)
2. **HTML statique** servi tel quel
3. **CSS inline** dans `<style>` (pas de fichier externe → -1 requête)
4. **JS minimal inline** : uniquement pour (a) toggle dark mode + `theme-color` meta, (b) CLI interactive (commandes, historique, fake exécution, redirection), (c) année dynamique du footer. Total < 3 Ko de JS.
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

> Je suis Benoît Dussaux, +15 ans dans la tech, un seul fil rouge : **la bonne solution, au vrai problème**.
>
> Au service des organisations à impact social et environnemental. Sans buzzword, sans techno-solutionnisme : juste du bon sens.
>
> Des outils qui marchent, pour des gens qui font.

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
3. **`prefers-reduced-motion`** : désactive le curseur clignotant, la rotation du widget WhatsApp et toutes les transitions CSS
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

1. Page 404 custom (si pas faite en v1)
2. `llms.txt` enrichi avec version `/llms-full.txt`
3. Animation ASCII au chargement (caractère par caractère)
4. Easter eggs CLI supplémentaires : `whoami`, `stack`, `sudo`, `joke`, etc.
5. Affinage du ton (manifeste, microcopy, fake-exécutions) après feedback réel

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
6. ✅ Photo affichée en cercle parfait dans le widget WhatsApp
7. ✅ Logo ASCII "BENOIT CODE" présent et lisible
8. ✅ JSON-LD Person valide (testé via validator.schema.org)
9. ✅ `robots.txt`, `sitemap.xml`, `llms.txt` présents
10. ✅ HTTPS forcé, HSTS activé
11. ✅ Test sur mobile (Safari iOS) et desktop (Chrome, Firefox)
12. ✅ Repo GitHub public, README rempli
13. ✅ CLI interactive fonctionnelle : 6 commandes (`linkedin`, `rdv`, `email`, `podcast`, `github`, `help`), chips cliquables, saisie clavier, historique ↑↓, persistance d'affichage en session
14. ✅ Widget WhatsApp flottant fonctionnel avec texte rotatif
15. ✅ Dark mode par défaut + toggle clair persistant en localStorage

---

## 12. Points ouverts à trancher

1. **Logo ASCII** : choix entre (a) statique, (b) animé caractère par caractère, (c) cyclique. → **Décision v1 : statique. Animation en v1.1 possible.**
2. **Manifeste** : ✅ tranché — version §6.2 validée.
3. **OG image** : la générer en SVG (ultra-light) ou WebP (plus universel) ? → à trancher en phase finalisation des assets.
4. **Affichage du score carbone** : ✅ tranché — Option A (badge statique mis à jour manuellement).
5. **Email affiché dans CLI / mailto** : Garder `bdussaux@gmail.com` ou créer une adresse pro type `hello@benoitdussaux.com` ? → à trancher.
6. **Easter eggs CLI** : ajout en v1 ou report v1.1 ? → **Décision : report v1.1**, on garde la CLI épurée sur les 6 commandes fonctionnelles.
