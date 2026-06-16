# Checklist — Base CRM (tags / segments / séquences)

> Objectif : poser une base CRM propre qui segmente et convertit automatiquement.
> Pour qui : créateurs, freelances, e-commerçants qui utilisent FluentCRM (ou équivalent).

## 1) Fondations
- [ ] Objectif business clair (vente / prise de RDV / fidélisation)
- [ ] Source(s) d'entrée listées (formulaire, achat, lead magnet)
- [ ] Double opt-in décidé (oui/non selon contexte + RGPD)
- [ ] Email expéditeur authentifié (SPF, DKIM, DMARC)

## 2) Convention de tags (rester simple)
- [ ] Tags de SOURCE (ex. `source-newsletter`, `source-achat`)
- [ ] Tags d'INTÉRÊT (ex. `interet-seo`, `interet-perf`)
- [ ] Tags d'ÉTAT (ex. `prospect`, `client`, `inactif`)
- [ ] Règle de nommage écrite et cohérente (minuscules, tirets)
- [ ] Éviter la sur-segmentation (commencer large)

## 3) Segments / listes
- [ ] 1 liste principale (newsletter)
- [ ] Segments dynamiques basés sur les tags (pas de tri manuel)
- [ ] Segment «clients» séparé du segment «prospects»
- [ ] Segment «inactifs» (90 j sans ouverture) pour réactivation

## 4) Séquences automatisées
- [ ] **Welcome** : 2 à 4 emails (valeur → preuve → offre douce)
- [ ] **Lead magnet** : livraison + relance si non ouvert
- [ ] **Post-achat** : onboarding / upsell
- [ ] **Réactivation** : relancer les inactifs avant nettoyage
- [ ] Conditions de sortie définies (ex. stop si achat)

## 5) Conformité
- [ ] Lien de désinscription dans chaque email
- [ ] Consentement tracé (date + source)
- [ ] Mention légale expéditeur visible

## 6) Mesure & entretien
- [ ] Taux d'ouverture / clic suivis par séquence
- [ ] Nettoyage trimestriel des contacts inactifs
- [ ] 1 test A/B en cours (objet ou CTA)
- [ ] Revue mensuelle des automations (ce qui convertit / à couper)
