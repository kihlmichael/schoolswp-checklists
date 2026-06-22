# SOP — Fabrique vidéo schoolsWP (HyperFrames)

**Objectif :** transformer un article / une page / un brief schoolsWP en vidéo courte rendue en MP4 (vertical 9:16 ou YouTube 16:9), de façon **répétable** et **pilotable par agent**.
Zéro blabla. Du process.

> HyperFrames = moteur « write HTML, render video » (HeyGen, licence Apache 2.0).
> Il **complète** HeyGen (avatar/voix), il ne le remplace pas. Combo : HeyGen = humain/voix · HyperFrames = motion design/overlays/graphiques · schoolsWP = contenu/scripts/templates.

---

## 0) Quand utiliser ce SOP
- [ ] Repurpose d’un article (« 3 erreurs… », « Plugin en 30 s », comparatif Gratuit/Pro)
- [ ] Annonce nouveauté plugin / WordPress
- [ ] Résumé d’un guide schoolsWP en Short vertical
- [ ] Carte / tableau comparatif animé pour LinkedIn / YouTube / X

---

## 1) Prérequis machine (one-time, sur le ROG Windows)
- [ ] **Node.js 22+** → `node --version` (si < 22, mettre à jour)
- [ ] **FFmpeg** installé et dans le PATH → `ffmpeg -version`
- [ ] GPU NVIDIA dispo (NVENC) pour l’encodage matériel via `--gpu`
- [ ] Diagnostic : `npx hyperframes doctor`

> Rendu **local** = meilleur pour itérer. **Docker** = à réserver au CI/CD / rendu déterministe partagé. Le rendu distribué (AWS Lambda) existe mais reste secondaire pour notre usage solo.

---

## 2) Installation & skills agent (one-time)
```bash
# Skill agent (Claude Code / Cursor / etc.) : apprend la boucle de production
npx skills add heygen-com/hyperframes

# Nouveau projet vidéo schoolsWP (avec Tailwind)
npx hyperframes init schoolswp-video --example blank --tailwind
cd schoolswp-video
```
- [ ] Skill installée
- [ ] Projet `schoolswp-video` créé et versionné (git)
- [ ] `npx hyperframes preview` ouvre bien la preview navigateur (hot reload)

---

## 3) Pipeline de production : article → vidéo
Une vidéo HyperFrames = un fichier **HTML** avec attributs `data-*`. Chaque élément `.clip` devient un clip sur une timeline. Animations : GSAP / CSS / Lottie / Three.js / Anime.js / WAAPI. Les compositions s’imbriquent.

### 3.1 Brief & script (agent)
- [ ] Source choisie : URL article schoolsWP / PDF / CSV / brief
- [ ] Angle unique défini (1 idée centrale)
- [ ] Script ≤ 20 s (hook 0–3 s → 1 à 3 points → CTA)
- [ ] Format cible : **9:16 (1080×1920)** par défaut · 16:9 si YouTube classique

### 3.2 Storyboard
- [ ] Découpage en scènes (durées en secondes)
- [ ] Identité visuelle schoolsWP : logo, couleurs, typo, URL
- [ ] Blocs catalogue à réutiliser repérés

### 3.3 Composition HTML
Squelette minimal (référence) :
```html
<div data-composition-id="schoolswp-short" data-width="1080" data-height="1920">
  <h1 class="clip" data-start="0" data-duration="3" data-track-index="1">
    3 erreurs WordPress
  </h1>
</div>
```
- [ ] `data-width` / `data-height` au bon ratio
- [ ] Chaque scène = un `.clip` avec `data-start` + `data-duration`
- [ ] Lower third « Michaël KIHL — schoolsWP » présent
- [ ] Outro avec URL (schoolswp.com) + CTA

### 3.4 Blocs du catalogue
```bash
npx hyperframes catalog            # parcourir (>50 blocs)
npx hyperframes add youtube-lower-third
npx hyperframes add data-chart
npx hyperframes add logo-outro
```
- [ ] Lower third ajouté
- [ ] Graphique / tableau animé si comparatif
- [ ] Transition + outro logo

### 3.5 Preview & lint
```bash
npx hyperframes preview
npx hyperframes validate
```
- [ ] Preview fluide (voir §5 si ça saccade)
- [ ] `validate` sans erreur
- [ ] Lisible **sans le son** (sous-titres / texte à l’écran)

---

## 4) Rendu (export MP4)
```bash
# Vertical 9:16, encodage GPU NVENC
npx hyperframes render --gpu --quality standard --output schoolswp-demo.mp4
```
- [ ] `--gpu` actif (NVENC) sur le ROG
- [ ] Bon `--output` (nommage : `aaaammjj_sujet_format.mp4`)
- [ ] Même entrée = même sortie (rendu déterministe : capture frame-par-frame via Chrome + FFmpeg)

---

## 5) QA avant publication
- [ ] Durée tenue (≤ 20 s pour un Short)
- [ ] Hook clair dans les 3 premières secondes
- [ ] Texte lisible mobile (taille, contraste, marges « safe »)
- [ ] Pas d’effet lourd qui casse le rendu : surveiller `backdrop-filter`, gros flous, ombres multiples, très grandes images
- [ ] Logo + lower third + outro + URL présents
- [ ] CTA unique et explicite

> La preview peut saccader sur frames coûteuses : le **rendu final** peut rester propre malgré ça. Juger sur l’export, pas sur la preview.

---

## 6) Publication & repurpose
- [ ] YouTube Shorts
- [ ] LinkedIn
- [ ] X
- [ ] Instagram Reels
- [ ] Espace membre / article d’origine (intégration)
- [ ] Lien retour vers l’article schoolsWP en description

---

## 7) Industrialisation : templates schoolsWP réutilisables
Créer une fois, ne changer que les **variables** (titre, plugin, prix, note, CTA, visuel, URL) :
- [ ] Intro schoolsWP
- [ ] Lower third « Michaël KIHL — schoolsWP »
- [ ] Carte « plugin » (nom / catégorie / verdict)
- [ ] Tableau comparatif animé (Gratuit vs Pro)
- [ ] Écran « avantage / limite / verdict »
- [ ] Outro URL + CTA
- [ ] Format « audit express »

---

## 8) Intégration agents (cible)
Agent dédié dans l’écosystème schoolsWP (cf. `schoolswp-telegram-agents` : Studio / Radar / Flow / Pulse) :

```
Agent : video-factory
Entrée : article schoolsWP | URL | PDF | CSV | brief
Sortie : script → storyboard → composition HTML → MP4 (+ version verticale + version YouTube)
```
- [ ] La CLI HyperFrames est non-interactive (flags + sorties texte) → adaptée à l’automatisation
- [ ] Skill `heygen-com/hyperframes` chargée côté agent
- [ ] Boucle agent : plan → HTML valide → animations seekables → médias → `validate` → `preview` → `render`

---

## 9) Dépannage rapide
| Symptôme | Action |
|---|---|
| `node` < 22 | Mettre à jour Node |
| `ffmpeg` introuvable | Installer FFmpeg + PATH, revérifier `ffmpeg -version` |
| Doute env | `npx hyperframes doctor` |
| Preview qui rame | Alléger effets (§5), juger sur le rendu final |
| Erreur de structure | `npx hyperframes validate` puis corriger les `data-*` |
| Rendu lent | Vérifier `--gpu` (NVENC) actif |

---

## Annexe — Référence commandes
| Commande | Rôle |
|---|---|
| `npx skills add heygen-com/hyperframes` | Installer la skill agent |
| `npx hyperframes init <projet> --example blank --tailwind` | Créer un projet |
| `npx hyperframes preview` | Preview navigateur (hot reload) |
| `npx hyperframes catalog` | Parcourir les blocs (>50) |
| `npx hyperframes add <bloc>` | Ajouter un bloc |
| `npx hyperframes validate` | Linter / valider la composition |
| `npx hyperframes render --gpu --quality standard --output <fichier>.mp4` | Rendre en MP4 |
| `npx hyperframes doctor` | Diagnostic environnement |

**Catalogue :** https://hyperframes.heygen.com/catalog
**Packages clés :** `hyperframes` (CLI) · `@hyperframes/core` · `@hyperframes/engine` (capture Chrome) · `@hyperframes/producer` (pipeline FFmpeg) · `@hyperframes/studio` · `@hyperframes/player` · `@hyperframes/shader-transitions`
