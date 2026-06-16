# Checklist — Audit SEO technique (les fondations)

Objectif : vérifier que Google peut **explorer**, **comprendre** et **indexer** le site sans friction, avant même de parler contenu.

## 1) Indexation & exploration
- [ ] Site indexable (Réglages > Lecture : case "décourager les moteurs" décochée)
- [ ] `robots.txt` propre (pas de blocage involontaire)
- [ ] Sitemap XML présent et soumis à Search Console
- [ ] Couverture Search Console : 0 erreur bloquante
- [ ] Pages "poubelle" (tags vides, archives inutiles) en noindex

## 2) Structure & URLs
- [ ] Permaliens propres (`/%postname%/`)
- [ ] 1 seul H1 par page
- [ ] Hiérarchie H2/H3 logique
- [ ] Profondeur de clic : pages clés à 3 clics max de l'accueil
- [ ] Fil d'Ariane (breadcrumb) actif

## 3) Contenu dupliqué & canonical
- [ ] Balise canonical correcte sur chaque page
- [ ] Pas de duplication www / non-www / http / https
- [ ] Pagination et filtres maîtrisés (canonical ou noindex)

## 4) Performance & mobile
- [ ] Core Web Vitals "good" (LCP, INP, CLS)
- [ ] Site responsive vérifié sur mobile réel
- [ ] Images compressées + lazy-load

## 5) Données structurées
- [ ] Schema Organisation / Person sur l'accueil
- [ ] Schema Article ou Product selon le type de page
- [ ] Test via l'outil de résultats enrichis : 0 erreur

## 6) Maillage & liens
- [ ] Pages stratégiques reçoivent des liens internes
- [ ] 0 lien interne cassé (404)
- [ ] Redirections 301 propres (pas de chaînes)
