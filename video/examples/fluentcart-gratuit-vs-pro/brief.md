# MVP vidéo — FluentCart Gratuit vs Pro

**Source :** https://schoolswp.com/fluentcart-gratuit-vs-pro/
**Format :** vertical 9:16 (1080×1920) · ~20 s · 30 fps
**Fichier composition :** `composition.html`

---

## Angle
Aider à trancher **Gratuit vs Pro** en 20 s : montrer ce que débloque la version Pro, puis donner un verdict net selon le profil.

## Script (voix off / sous-titres)
| t | Texte |
|---|---|
| 0–3 s | « FluentCart : Gratuit ou Pro ? Voici ce qui change vraiment. » |
| 3–7 s | « Le Pro débloque les tunnels de vente — upsells, downsells — et les abonnements avancés. » |
| 7–11 s | « Plus les licences logicielles et des rapports détaillés par produit et client. » |
| 11–14 s | « Et surtout : FluentCRM poussé, avec des automatisations marketing selon l'achat. » |
| 14–17 s | « Gratuit si tu débutes simple. Pro si tu vises la croissance. » |
| 17–20 s | « Le guide complet est sur schoolswp.com. » |

## Storyboard
1. **Hook** — titre « Gratuit vs Pro ? »
2. **Réservé au Pro (1/2)** — cartes : Tunnels de vente · Abonnements avancés
3. **Réservé au Pro (2/2)** — cartes : Licences logicielles · Rapports avancés
4. **Atout décisif** — carte : intégration FluentCRM
5. **Verdict** — 2 lignes : Gratuit (débutant) / Pro (croissance)
6. **Outro** — logo schoolsWP + URL + CTA
- **Lower third** « Michaël KIHL — schoolsWP » persistant tout du long.

## 5 différentiateurs Pro (issus de l'article)
1. Tunnels de vente (upsells/downsells post-achat)
2. Gestion avancée des abonnements (frais d'installation, essais, synchro CRM)
3. Génération de licences logicielles
4. Rapports avancés (segmentation produit/client vs 30 j en gratuit)
5. Intégration FluentCRM poussée (déclencheurs marketing)

## Verdict de l'article
- **Gratuit suffit** : freelance / créateur, produits simples, pas de scaling.
- **Pro s'impose** : croissance, automatisation marketing, abonnements complexes.
- **Reco** : commencer gratuit, migrer au besoin.

---

## À lancer sur le ROG
```bash
git pull origin claude/hyperframes-schoolswp-analysis-46hxs6
# place composition.html dans ton projet hyperframes (ou pointe-le)
npx hyperframes validate
npx hyperframes preview
npx hyperframes render --gpu --quality standard --output fluentcart-gratuit-vs-pro_9x16.mp4
```

## Branding (v3 — charte officielle schoolsWP)
- **Vert accent** `#00d400` (vif) / `#00a100` (foncé) sur **fond sombre** `#12111f` / `#212121`.
- Gris froids `#57556d` / `#8f8da5` pour le texte secondaire ; blancs `#fafbfd` / `#f4f6fb`.
- **Logo officiel** (white) dans l'outro et le lower third (plus de texte « schoolsWP »).
  - URL blanche : `https://schoolswp.com/wp-content/uploads/2022/06/cropped-cropped-logo-schoolsWP-nom-white-sans-contour.png`
  - URL noire : `https://schoolswp.com/wp-content/uploads/2022/06/logo-schoolsWP-nom-black-sans-contour-1.png`
- Pro = vert schoolsWP · Gratuit = gris froid. Vert sur kicker, labels, badges, tag Pro, URL.

## Réglages à vérifier / ajuster
- [ ] **Logo en local** : pour un rendu hors-ligne/déterministe, télécharge le PNG dans le projet et remplace l'URL par un chemin local (`./assets/logo-schoolswp.png`).
- [ ] Police : `Inter` (fallback système) — embarquer la vraie webfont schoolsWP si tu veux le rendu exact.
- [ ] Lisibilité mobile (taille texte, marges safe) — juger sur le **rendu final**, pas la preview.
- [ ] Durées par scène (`data-duration`) à affiner après la 1re preview.
- [ ] Voix off : ajouter une piste audio (TTS / HeyGen) si tu veux du son.
- [ ] Syntaxe `data-*` : confirmer qu'elle correspond au runtime HyperFrames installé (sinon adapter selon `catalog`/exemples du repo).
