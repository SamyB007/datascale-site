# datascale.fr

Site vitrine de DATA SCALE — HTML statique, charte v2.2, hébergé sur GitHub Pages. Intro animée, accueil en particules (canvas), schéma vivant de la plateforme en quatre couches (SVG), défilement fluide et animations au scroll (GSAP, ScrollTrigger, Lenis, hébergés dans `assets/js/`).

## Contenu du dépôt

| Fichier | Rôle |
| --- | --- |
| `index.html` | Page d'accueil (one-page) : démarche, plateforme (Cloud, Data, IA, Run), modes d'engagement, références, contact |
| `mentions-legales.html` | Mentions légales |
| `404.html` | Page introuvable |
| `CNAME` | Domaine personnalisé `datascale.fr` (ne pas supprimer) |
| `.nojekyll` | Désactive le traitement Jekyll de GitHub Pages |
| `robots.txt`, `sitemap.xml` | Référencement |
| `favicon.svg`, `favicon-32.png`, `apple-touch-icon.png` | Icônes (logo 2024) |
| `assets/fonts/` | Schibsted Grotesk et Martian Mono, auto-hébergées (pas d'appel à Google Fonts) |
| `assets/js/` | GSAP 3.12.5, ScrollTrigger et Lenis 1.1.20, auto-hébergés |
| `assets/img/` | Logo, image de partage `og-image.png` |

Aucun cookie, aucun outil de mesure d'audience, aucun appel à un service tiers : polices et bibliothèques sont servies par le site lui-même. Sans JavaScript ou avec « réduire les animations » activé, le site reste entièrement lisible, sans intro ni animation.

## Mise en ligne — GitHub Pages

1. Créer un dépôt **public** (GitHub Pages avec domaine personnalisé exige un dépôt public sur un compte Free), par exemple `datascale-site`.
2. Y déposer l'intégralité de ce dossier à la racine (interface web « Add file → Upload files », ou `git push`).
3. **Settings → Pages** : *Source* = « Deploy from a branch », branche `main`, dossier `/ (root)`. Enregistrer.
4. Dans la même page, **Custom domain** : `datascale.fr` → *Save*. GitHub vérifie le DNS (voir ci-dessous), puis cocher **Enforce HTTPS** dès que la case est disponible (certificat Let's Encrypt émis en quelques minutes à quelques heures).
5. Chaque modification poussée sur `main` est en ligne en une minute environ.

Recommandé : vérifier le domaine au niveau du compte (**Settings → Pages → Add a domain**), ce qui ajoute un enregistrement TXT `_github-pages-challenge-<utilisateur>` et empêche toute reprise du domaine par un autre dépôt.

## DNS — Squarespace Domains (datascale.fr)

Dans Squarespace → Domaines → datascale.fr → **Paramètres DNS**, ajouter (sans toucher aux enregistrements MX et TXT existants de Google Workspace) :

| Type | Hôte | Valeur | TTL |
| --- | --- | --- | --- |
| A | `@` | `185.199.108.153` | 1 h |
| A | `@` | `185.199.109.153` | 1 h |
| A | `@` | `185.199.110.153` | 1 h |
| A | `@` | `185.199.111.153` | 1 h |
| AAAA | `@` | `2606:50c0:8000::153` | 1 h |
| AAAA | `@` | `2606:50c0:8001::153` | 1 h |
| AAAA | `@` | `2606:50c0:8002::153` | 1 h |
| AAAA | `@` | `2606:50c0:8003::153` | 1 h |
| CNAME | `www` | `<utilisateur-github>.github.io.` | 1 h |

Supprimer tout enregistrement A ou CNAME préexistant sur `@` et `www` (page de parking Squarespace). Propagation : quelques minutes à quelques heures. `www.datascale.fr` redirigera vers `datascale.fr`.

Vérification : `dig datascale.fr +short` doit renvoyer les quatre adresses 185.199.x.153.

## Authentification des e-mails (« Action requise » dans Google Admin)

À faire pour **datascale.fr** et **datascaleac.com**, chez le registrar de chaque domaine :

| Type | Hôte | Valeur |
| --- | --- | --- |
| TXT | `@` | `v=spf1 include:_spf.google.com ~all` |
| TXT | `google._domainkey` | clé générée dans Google Admin → Applications → Google Workspace → Gmail → Authentifier les e-mails → sélectionner le domaine → *Générer un enregistrement* (2048 bits), puis *Lancer l'authentification* une fois le TXT publié |
| TXT | `_dmarc` | `v=DMARC1; p=none; rua=mailto:dmarc@datascaleac.com` — passer à `p=quarantine` après quelques semaines de rapports propres |

## Mettre à jour le contenu

Tout le contenu est dans `index.html` (texte en clair, une section par bloc `<section>`). Les offres de chaque couche sont dans les panneaux `p-cloud`, `p-data`, `p-ia` et `p-run` ; les références dans le bloc `.wall`. Aucune compilation nécessaire.
