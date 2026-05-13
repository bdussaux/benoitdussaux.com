# Contexte projet — benoitdussaux.com

## Stack
- HTML/CSS/JS vanilla, **aucun build, aucun framework**
- Hébergement Netlify (free tier), DNS OVH
- Versioning : GitHub `bdussaux/benoitdussaux.com`

## Contraintes strictes
- **Frugal by design** : viser < 100 Ko total, score WebsiteCarbon A+
- CSS et JS inline dans `index.html` (pas de fichiers externes pour économiser des requêtes)
- Aucune dépendance tierce (pas de CDN, pas de Google Fonts, pas d'analytics)
- Font JetBrains Mono self-hosted (woff2 subset latin)
- Photo unique en WebP optimisé
- Respecter `prefers-reduced-motion`
- Accessibilité : Lighthouse 100/100 visé

## Identité
- Style terminal façon Claude Code
- Dark mode par défaut, toggle clair possible
- Palette : accent orange Claude (#D97757 dark / #C96342 light)
- Ton : auto-dérision douce, sec, geek assumé
- Police unique : JetBrains Mono

## Specs complètes
Voir `docs/PRD.md` pour le PRD versionné.

## Ce qui reste à faire (v1)
- [ ] Ajouter photo.webp (160×160 source, servie 80×80)
- [ ] Ajouter font JetBrains Mono woff2 dans /fonts/
- [ ] Créer 404.html
- [ ] Créer robots.txt, sitemap.xml, llms.txt
- [ ] Créer netlify.toml (headers cache + sécurité)
- [ ] Générer og.webp (1200×630)
- [ ] Mesurer score WebsiteCarbon réel et mettre à jour le badge

## Workflow
Push sur `main` = déploiement auto Netlify.
