# Checklist — Sécurité & hardening WordPress

Objectif : réduire la surface d'attaque et garantir une récupération rapide en cas de problème. À passer à la mise en prod, puis à revérifier tous les trimestres.

## 1) Accès & comptes
- [ ] Aucun utilisateur "admin" par défaut
- [ ] Mots de passe forts + uniques (gestionnaire de mots de passe)
- [ ] Authentification à deux facteurs (2FA) sur les comptes admin
- [ ] Rôles utilisateurs au plus juste (principe du moindre privilège)
- [ ] Suppression des comptes inactifs

## 2) Connexion
- [ ] Limitation des tentatives de connexion
- [ ] Protection anti-bruteforce / pare-feu (WAF)
- [ ] URL de connexion non triviale (optionnel)

## 3) Cœur, thèmes & extensions
- [ ] Cœur WordPress à jour
- [ ] Thèmes et extensions à jour
- [ ] Suppression des thèmes/extensions inactifs
- [ ] Aucune extension nulled / piratée
- [ ] Édition de fichiers désactivée (`DISALLOW_FILE_EDIT`)

## 4) Serveur & fichiers
- [ ] SSL actif + forçage HTTPS
- [ ] Permissions fichiers correctes (644) et dossiers (755)
- [ ] `wp-config.php` protégé
- [ ] Versions PHP supportées uniquement
- [ ] Headers de sécurité (HSTS, X-Frame-Options, etc.)

## 5) Sauvegardes & récupération
- [ ] Sauvegardes automatiques (fichiers + base)
- [ ] Sauvegardes stockées hors-serveur
- [ ] Restauration testée au moins une fois
- [ ] RTO/RPO connus (combien de temps / combien de données max perdues)

## 6) Surveillance
- [ ] Scan de malware actif
- [ ] Alertes sur modifications de fichiers
- [ ] Journal des connexions admin
- [ ] Monitoring de disponibilité (uptime)
