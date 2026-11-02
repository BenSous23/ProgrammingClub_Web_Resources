# 🛠 Guide d'installation — VS Code, Git & GitHub

Guide pas à pas pour préparer ton environnement de développement avant la S1.
**Durée estimée : 30 à 45 min.** À faire **avant** la séance si possible.

## Sommaire

1. [Créer un compte GitHub](#1-créer-un-compte-github)
2. [Installer VS Code](#2-installer-vs-code)
3. [Installer Git](#3-installer-git)
4. [Configurer Git](#4-configurer-git)
5. [Vérifier que tout fonctionne](#5-vérifier-que-tout-fonctionne)
6. [Extensions VS Code recommandées](#6-extensions-vs-code-recommandées)
7. [Blocages fréquents et solutions](#7-blocages-fréquents-et-solutions)
8. [Checklist finale](#8-checklist-finale)

---

## 1. Créer un compte GitHub

1. Va sur **https://github.com/signup**
2. Choisis un **username** professionnel (ex : `prenom-nom`, `pnom`). Il apparaîtra sur ton portfolio. Évite les pseudos fantaisistes.
3. Utilise une **adresse email valide** que tu consultes régulièrement.
4. Valide le compte (captcha + code par email).
5. **Vérifie ton email** : sans cette étape, les `push` échouent silencieusement plus tard.

**Vérification :** tu peux te connecter sur github.com et voir ton profil à l'adresse `https://github.com/TON_USERNAME`.

---

## 2. Installer VS Code

### Windows

1. Télécharge l'installateur : **https://code.visualstudio.com/download** → bouton **Windows**.
2. Lance le fichier `.exe`.
3. Pendant l'installation, coche ces cases :
   - ✅ *Add "Open with Code" action to Windows Explorer file context menu*
   - ✅ *Add "Open with Code" action to Windows Explorer directory context menu*
   - ✅ *Add to PATH* (généralement coché par défaut)
4. Termine l'installation.

### macOS

1. Télécharge : **https://code.visualstudio.com/download** → choisis **Apple Silicon** (M1/M2/M3) ou **Intel** selon ton Mac.
2. Ouvre le `.zip` → glisse **Visual Studio Code.app** dans **Applications**.
3. Ouvre VS Code → **View → Command Palette** (`Cmd+Shift+P`) → tape `Shell Command: Install 'code' command in PATH` → Entrée.

### Linux (Debian / Ubuntu)

```bash
sudo apt update
sudo apt install code
```

Ou via le paquet `.deb` téléchargé depuis le site officiel :

```bash
sudo dpkg -i code_*.deb
```

**Vérification :** VS Code s'ouvre et affiche l'écran de bienvenue.

---

## 3. Installer Git

### Windows

1. Télécharge : **https://git-scm.com/download/win** (l'installateur 64-bit se lance automatiquement).
2. Lance l'installateur. Garde les options par défaut, sauf :
   - Écran *Adjusting your PATH environment* → laisse **"Git from the command line and also from 3rd-party software"**.
   - Écran *Choosing the default editor used by Git* → choisis **"Use Visual Studio Code as Git's default editor"**.
3. Termine l'installation.

### macOS

Deux options :

- **La plus simple** : ouvre le Terminal, tape `git --version`. Si Git n'est pas installé, macOS propose de l'installer (outils de développement Apple). Accepte.
- **Version récente** : installe via Homebrew avec `brew install git`.

### Linux (Debian / Ubuntu)

```bash
sudo apt update
sudo apt install git
```

**Vérification :** ouvre un **nouveau** terminal (ou redémarre VS Code) et tape :

```bash
git --version
```

Tu dois voir quelque chose comme `git version 2.43.0`. Si la commande n'est pas reconnue, va à la section 7.

---

## 4. Configurer Git

Ouvre un terminal (ou le terminal intégré de VS Code : `` Ctrl+` ``) et tape les commandes suivantes en remplaçant par tes informations :

```bash
git config --global user.name "Prénom Nom"
git config --global user.email "ton-email@exemple.com"
```

⚠️ **Utilise le même email que celui de ton compte GitHub.** Sinon tes commits ne seront pas liés à ton profil.

Options recommandées :

```bash
# Nom de branche par défaut moderne
git config --global init.defaultBranch main

# Éditeur par défaut
git config --global core.editor "code --wait"
```

**Vérification :**

```bash
git config --global --list
```

Tu dois voir `user.name` et `user.email` avec tes valeurs.

---

## 5. Vérifier que tout fonctionne

### Test 1 — Cloner un dépôt

```bash
cd ~/Documents
git clone https://github.com/TON_USERNAME/s1-hello.git
cd s1-hello
```

### Test 2 — Ouvrir dans VS Code

```bash
code .
```

VS Code doit s'ouvrir sur le dossier `s1-hello`.

### Test 3 — Modifier et pousser

1. Dans VS Code, ouvre `README.md` et ajoute une ligne avec ton prénom.
2. Sauvegarde avec `Ctrl+S` (ou `Cmd+S` sur macOS).
3. Dans le terminal intégré, exécute :

```bash
git add README.md
git commit -m "ajout de mon prénom"
git push
```

4. Va sur GitHub, ouvre `s1-hello` : ton commit doit apparaître.

**Si les 3 tests passent, tu es prêt pour la S1.**

---

## 6. Extensions VS Code recommandées

Ouvre VS Code → icône **Extensions** (ou `Ctrl+Shift+X` / `Cmd+Shift+X`) → cherche et installe :

| Extension | Auteur | Utilité |
|---|---|---|
| **Live Server** | Ritwick Dey | Aperçu HTML en direct avec rechargement automatique |
| **Prettier - Code formatter** | Prettier | Formate automatiquement ton code |
| **GitLens** | GitKraken | Voir l'historique Git directement dans l'éditeur |
| **French Language Pack** | Microsoft | Interface VS Code en français (optionnel) |
| **ESLint** | Microsoft | Détecte les erreurs JavaScript (utile dès S4) |

**Astuce Prettier** : après installation, ouvre les paramètres (`Ctrl+,`), cherche `Format On Save` et coche la case. Ton code sera formaté à chaque sauvegarde.

---

## 7. Blocages fréquents et solutions

### `git : commande introuvable` ou `'git' is not recognized`

**Cause :** Git n'est pas dans le PATH, ou le terminal n'a pas été redémarré après installation.

**Solution :**

1. **Ferme complètement** VS Code et tous les terminaux ouverts.
2. Rouvre un terminal et retape `git --version`.
3. Si ça persiste sur Windows : réinstalle Git en cochant bien **"Git from the command line and also from 3rd-party software"**.
4. Sur Windows, tu peux aussi utiliser **Git Bash** (installé avec Git) au lieu de PowerShell.

### `Permission denied (publickey)` au `push`

**Cause :** tu utilises une URL SSH (`git@github.com:...`) sans clé SSH configurée.

**Solution simple :** utilise l'URL HTTPS. Sur GitHub, bouton **Code** → onglet **HTTPS** → copie l'URL `https://github.com/...`. Reclone avec cette URL, ou change l'URL distante :

```bash
git remote set-url origin https://github.com/TON_USERNAME/s1-hello.git
```

### `Authentication failed` au `push`

**Cause :** GitHub n'accepte plus le mot de passe simple depuis 2021.

**Solution :** utilise un **Personal Access Token (PAT)**.

1. GitHub → **Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)** → **Generate new token**.
2. Coche la portée `repo` (et `workflow` si besoin).
3. Copie le token (il ne s'affiche qu'une seule fois).
4. Au moment du `push`, quand Git demande le mot de passe, colle le token à la place.

Alternative : installe **GitHub Desktop** ou utilise **VS Code** avec l'extension **GitHub Pull Requests and Issues** qui gère l'authentification en un clic.

### `fatal: not a git repository`

**Cause :** tu es dans un dossier qui n'est pas un dépôt Git.

**Solution :** fais `cd` dans le bon dossier (celui qui contient un `.git/` caché), ou clone le dépôt si ce n'est pas encore fait.

### Email GitHub non vérifié → `push` silencieusement bloqué

**Solution :** GitHub → **Settings** → **Emails** → vérifie que ton email est confirmé (badge vert *Verified*).

### VS Code ne trouve pas `code` dans le terminal (macOS)

**Solution :** `Cmd+Shift+P` → `Shell Command: Install 'code' command in PATH` → Entrée.

### Wi-Fi universitaire bloque GitHub

**Solution :** utilise le partage de connexion de ton téléphone pour la S1, ou demande le réseau invité. En dernier recours, on travaillera sur CodePen / StackBlitz (aucune installation requise).

---

## 8. Checklist finale

Avant la S1, vérifie que tout est coché :

- [ ] Compte GitHub créé et email vérifié
- [ ] VS Code installé et s'ouvre
- [ ] `git --version` affiche une version dans un terminal
- [ ] `git config --global user.name` et `user.email` configurés avec le **même email** que GitHub
- [ ] Extension **Live Server** installée dans VS Code
- [ ] Extension **Prettier** installée et *Format On Save* activé
- [ ] `git clone https://github.com/TON_USERNAME/s1-hello.git` fonctionne
- [ ] `code .` ouvre le dossier dans VS Code
- [ ] Un commit + push de test apparaît sur GitHub

Si un point bloque, note le message d'erreur **exact**, apporte-le en S1 ou poste-le sur le canal du club.

---

## Besoin d'aide avant la S1 ?

- Poste ton message d'erreur **exact** (copie-colle, pas de capture floue) sur le canal du club.
- Précise ton OS (Windows / macOS / Linux) et la version de Git (`git --version`).
- En dernier recours, viens 15 min en avance en S1 : on déboguera ensemble.

Bon courage — une fois cette étape passée, tout le reste du semestre devient plus fluide. 🚀