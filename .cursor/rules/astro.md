# Guide de Développement - Site Astro

## Structure du Projet

- `src/content/` - Contenu structuré (articles, projets)
- `src/components/` - Composants réutilisables
- `src/layouts/` - Layouts de pages
- `src/pages/` - Pages et routes
- `src/styles/` - Styles globaux et utilitaires
- `public/` - Assets statiques (images, fonts, etc.)
- `src/utils/` - Fonctions utilitaires
- `src/types/` - Types TypeScript

## Conventions de Nommage
- Fichiers de contenu: kebab-case `.md` ou `.mdx` (ex: `mon-projet.md`)
- Composants: PascalCase `.astro` ou `.tsx` (ex: `ProjectCard.astro`)
- Layouts: PascalCase avec suffixe "Layout" (ex: `BaseLayout.astro`)
- Utils: camelCase (ex: `formatDate.ts`)

## Frontmatter des Contenus
```yaml
---
title: Titre du contenu
description: Description SEO-friendly
pubDate: YYYY-MM-DD
updatedDate: YYYY-MM-DD # optionnel
author: Jimmy Gilbert
image:
  src: /assets/images/mon-image.jpg
  alt: Description de l'image
tags: [tag1, tag2]
draft: false
---
```

## Bonnes Pratiques Astro

### Performance

- Utiliser `<Image />` d'Astro pour l'optimisation automatique des images
- Implémenter le View Transitions API pour les transitions fluides
- Préférer les composants `.astro` aux composants framework quand possible
- Utiliser `client:load` uniquement quand nécessaire
- Mettre en place le prefetching intelligent avec `prefetch`

### SEO

- Utiliser les métadonnées dynamiques avec `<SEO />`
- Implémenter une sitemap.xml automatique
- Configurer le robots.txt
- Assurer des URLs propres et descriptives
- Mettre en place les balises Open Graph

### Collections

```typescript
// src/content/config.ts
import { defineCollection, z } from "astro:content";

const projects = defineCollection({
  type: "content",
  schema: z.object({
    title: z.string(),
    description: z.string(),
    pubDate: z.date(),
    updatedDate: z.date().optional(),
    author: z.string().default("Jimmy Gilbert"),
    image: z.object({
      src: z.string(),
      alt: z.string(),
    }),
    tags: z.array(z.string()),
    draft: z.boolean().default(false),
  }),
});

export const collections = { projects };
```

### Composants Essentiels

- `<BaseHead />` - Métadonnées communes et SEO
- `<Navigation />` - Navigation responsive
- `<Footer />` - Pied de page commun
- `<ProjectCard />` - Carte de présentation de projet
- `<TagList />` - Liste de tags avec filtrage
- `<Pagination />` - Navigation entre les pages

## Style et Design

### Framework CSS

- Bootstrap 5 comme framework principal
- Variables CSS pour la thématisation

### Accessibilité

- Respecter WCAG 2.1 niveau AA
- Tester avec les lecteurs d'écran
- Assurer une navigation au clavier
- Maintenir un contraste suffisant
- Utiliser des attributs ARIA appropriés

### Responsive Design

- Mobile-first approach
- Points de rupture Bootstrap standards
- Images responsive avec art direction
- Tester sur multiples appareils

## Déploiement

- Utiliser un CDN pour les assets statiques
- Mettre en cache les assets appropriés
- Compresser les assets (gzip/brotli)
- Surveiller les performances avec Lighthouse
- Maintenir un score PageSpeed optimal
