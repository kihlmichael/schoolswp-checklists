# Checklist — Mise en production WordPress (go-live pro)

> Objectif : passer un site en ligne sans casse, propre et indexable.
> Pour qui : freelances, agences, propriétaires de sites WordPress.

## 1) Avant la bascule
- [ ] Sauvegarde complète (fichiers + base de données)
- [ ] Environnement de staging validé (visuel + fonctionnel)
- [ ] Liste des URLs critiques recensée (pages, tunnels, formulaires)
- [ ] Plan de redirections 301 prêt (ancien → nouveau)
- [ ] Emails transactionnels testés (FluentSMTP / SMTP dédié)

## 2) Technique
- [ ] PHP à jour (version supportée)
- [ ] HTTPS actif + redirection HTTP → HTTPS
- [ ] Permaliens propres (pas d'`?p=123`)
- [ ] Cache configuré (FlyingPress / équivalent) et purgé
- [ ] Images optimisées (WebP, lazy-load)
- [ ] Favicon + métadonnées Open Graph

## 3) SEO & indexation
- [ ] `noindex` de staging RETIRÉ (réglage Lecture)
- [ ] Sitemap XML généré (Rank Math) et soumis à Search Console
- [ ] robots.txt vérifié (rien de bloquant)
- [ ] Balises title / meta des pages clés en place
- [ ] Données structurées validées (Rich Results Test)

## 4) Conformité & sécurité
- [ ] Bandeau cookies / RGPD actif
- [ ] Mentions légales + politique de confidentialité publiées
- [ ] Sécurité activée (SecuPress / pare-feu)
- [ ] Comptes admin : mots de passe forts + 2FA

## 5) Après go-live (J+0 à J+3)
- [ ] Test parcours complet (achat / contact / inscription)
- [ ] Vérif mobile + Core Web Vitals (PageSpeed)
- [ ] Liens cassés contrôlés
- [ ] Sauvegarde automatique programmée
- [ ] Monitoring uptime activé
