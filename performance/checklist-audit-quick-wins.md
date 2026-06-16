# Checklist — Audit performance WordPress (Quick Wins)

> Objectif : gagner en vitesse rapidement, sans refonte.
> Pour qui : sites lents qui veulent des résultats mesurables vite.

## 1) Mesure de départ
- [ ] Score PageSpeed Insights (mobile + desktop) noté
- [ ] Core Web Vitals relevés (LCP, INP, CLS)
- [ ] Poids total de la page d'accueil mesuré

## 2) Images (souvent le plus gros gain)
- [ ] Conversion en WebP
- [ ] Compression activée
- [ ] Lazy-load des images hors écran
- [ ] Dimensions correctes (pas d'image 4000px affichée en 400px)

## 3) Cache & livraison
- [ ] Cache de page activé (FlyingPress / équivalent)
- [ ] CDN actif pour les fichiers statiques
- [ ] Compression GZIP / Brotli active

## 4) CSS / JS
- [ ] Minification CSS + JS
- [ ] Différer le JS non critique
- [ ] Supprimer les CSS/JS inutilisés (ex. emoji, scripts inutiles)
- [ ] Précharger les polices critiques

## 5) Nettoyage
- [ ] Extensions inutiles désactivées et supprimées
- [ ] Base de données optimisée
- [ ] Réduire les requêtes externes (fonts, trackers)

## 6) Vérification finale
- [ ] Nouveau score PageSpeed comparé au départ
- [ ] Test sur mobile réel
- [ ] Aucun élément cassé (visuel + fonctionnel)
