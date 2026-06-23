# HyperFrames `pr-to-video` — Installation, Test, Sécurité & Veille

> Procédure schoolsWP pour installer et tester le skill **`pr-to-video`** du dépôt
> [`heygen-com/hyperframes`](https://github.com/heygen-com/hyperframes), puis mettre en place une veille.
> Environnement cible : **Windows-first** (PowerShell). Niveau : non-développeur, étape par étape.
> Dernière vérification du dépôt : 2026-06-23.

---

## 0. Faits vérifiés sur le dépôt réel

| Élément | Valeur réelle |
|---|---|
| Prérequis | **Node.js 22+** et **FFmpeg** (obligatoires) |
| Install skills (agents IA) | `npx skills add heygen-com/hyperframes` |
| Init projet manuel | `npx hyperframes init my-video` |
| Preview / Rendu | `npx hyperframes preview` / `npx hyperframes render` |
| Clé API | **HeyGen** requise **uniquement** pour l'audio (TTS + musique) de `pr-to-video`, lue dans `~/.heygen`. Le rendu de base ne demande aucune clé. |
| `pr-to-video` exige | **GitHub CLI `gh` authentifié** avec accès à la PR |
| Formats | 16:9 `1920x1080` (défaut), 9:16 `1080x1920`, 1:1 `1080x1080` |
| Licence | Apache 2.0 (usage commercial OK) |
| Clone complet | nécessite **Git LFS** (sinon `GIT_LFS_SKIP_SMUDGE=1 git clone ...`) |
| Style visuel `pr-to-video` | toujours **« claude »** (non modifiable) |

---

## 1. Vérifier les prérequis (PowerShell)

```powershell
node -v          # v22.x.x ou plus
npm -v
git --version
gh --version
gh auth status   # doit être authentifié
ffmpeg -version
```

Installation si manquant (winget) :

```powershell
winget install OpenJS.NodeJS.LTS   # Node.js LTS >= 22
winget install Git.Git
winget install GitHub.cli
winget install Gyan.FFmpeg
```

Puis **fermer/rouvrir PowerShell** et relancer les `-v`. Authentifier GitHub : `gh auth login`.

---

## 2. Installation isolée (jamais dans les repos schoolsWP)

```powershell
mkdir $HOME\hyperframes-lab
cd $HOME\hyperframes-lab
npx skills add heygen-com/hyperframes   # Mode B : skills pour agent IA
```

> `npx` exécute sans installation globale permanente.

---

## 3. Test minimal du rendu de base (Mode A)

```powershell
cd $HOME\hyperframes-lab
npx hyperframes init test-video --non-interactive --example blank
cd test-video
npx hyperframes preview                       # aperçu navigateur
npx hyperframes render --output renders\test.mp4
```

✅ Critère : `renders\test.mp4` se lit → chaîne Node + FFmpeg + Chrome OK.

---

## 4. Test du skill `pr-to-video`

Prérequis : `gh auth status` ✅, clé HeyGen dans `~/.heygen`, **PR PUBLIQUE non sensible**.

`pr-to-video` est un skill d'agent IA (Claude Code / Cursor…), pas une commande shell. Prompt de test :

```
Using /pr-to-video, create a 45-60 second French vertical (9:16) video from this PUBLIC GitHub PR:
[URL_DE_LA_PR_PUBLIQUE]

Audience: WordPress creators, freelancers, trainers, solo builders.
Angle: infer (fix-explainer or feature-reveal).
Goal: explain what changed, why it matters, what the user can now do better.
Rules:
- Not developer-heavy. Don't narrate files one by one.
- Explain the practical benefit. Simple French. Short script.
- End with a clear takeaway, not a sales CTA.
Style: schoolsWP — clear, calm, useful, no hype.
```

Sortie : `renders/video.mp4`. **Critère MVP :** compréhensible par un non-développeur.

---

## 5. Sécurité

| Risque | Règle |
|---|---|
| Clé API | La clé HeyGen vit **uniquement** dans `~/.heygen` ; jamais dans un prompt/commit. `.heygen` dans `.gitignore`. |
| PR sensible | 1er test = PR publique. Pour `schoolswp-os` privé : relire le diff avant, zéro secret. |
| Fichiers lus | Vérifier `capture/extracted/` ; le diff complet passe dans le contexte de l'agent. |
| Isolation | Tout dans `$HOME\hyperframes-lab`, jamais dans un repo schoolsWP. |
| Réseau | Le script narratif final est envoyé à HeyGen (TTS) ; pas d'info confidentielle dedans. |

---

## 6. Veille — 3 options

### Option 1 — Simple (GitHub natif) ★☆☆
GitHub → repo → **Watch** → **Custom** → cocher **Releases** (+ Discussions). 5 min.

### Option 2 — RSS / Atom ★★☆
Ajouter dans un lecteur RSS :
- Releases : `https://github.com/heygen-com/hyperframes/releases.atom`
- Commits main : `https://github.com/heygen-com/hyperframes/commits/main.atom`
- **Commits du skill** : `https://github.com/heygen-com/hyperframes/commits/main/skills/pr-to-video.atom`
- Tags : `https://github.com/heygen-com/hyperframes/tags.atom`

### Option 3 — Automatisé (n8n + GitHub API + Telegram) ★★★
Cron quotidien → GitHub API (commits sur `skills/pr-to-video` + releases) → IF nouveau (dernier SHA stocké) → résumé IA → Telegram.
Résumé : *ce qui a changé / impact schoolsWP / urgence / action recommandée*.

---

## 7. Checklist de validation

```
ENVIRONNEMENT
[ ] Node.js v22+        (node -v)
[ ] npm / npx           (npm -v)
[ ] Git                 (git --version)
[ ] GitHub CLI gh       (gh --version)
[ ] gh authentifié      (gh auth status)
[ ] FFmpeg              (ffmpeg -version)

INSTALLATION
[ ] Dossier isolé créé  ($HOME\hyperframes-lab)
[ ] Skills installés    (npx skills add heygen-com/hyperframes)

RENDU DE BASE
[ ] init OK
[ ] preview OK
[ ] render MP4 OK (renders\test.mp4 se lit)

PR-TO-VIDEO
[ ] Clé HeyGen dans ~/.heygen (jamais committée)
[ ] PR PUBLIQUE choisie pour le 1er test
[ ] Vidéo 9:16 FR générée
[ ] Comprise par un NON-développeur

SÉCURITÉ
[ ] .heygen dans .gitignore
[ ] Aucun secret dans le prompt / script narratif
[ ] Tests isolés du repo schoolswp-os
[ ] Contenu de capture/extracted/ vérifié

VEILLE
[ ] Option 1 (Watch GitHub : Releases) active
[ ] Option 2 (flux .atom dans lecteur RSS) ajoutée
[ ] Canal d'alerte décidé (n8n+Telegram OU /loop Claude)
[ ] Procédure documentée (ce fichier)
```

---

## 8. Décision

**GO pour le MVP isolé** (PR publique → vidéo 9:16 FR → test compréhension).
**WAIT pour l'intégration production** dans le pipeline YouTube principal.
Pour le grand public WordPress, toujours ajouter la couche éditoriale « ce que ça change pour toi », pas « voici le diff ».
