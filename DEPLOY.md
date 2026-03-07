# Publier le site (Vercel, Netlify, GitHub Pages)

L’application est **100 % statique** (un fichier HTML + scripts chargés en CDN). Aucun serveur ni base de données : tu peux la déployer gratuitement sur plusieurs plateformes.

---

## Vercel (recommandé)

1. **Compte**  
   Crée un compte sur [vercel.com](https://vercel.com) (avec GitHub, GitLab ou email).

2. **Projet**  
   - Va sur [vercel.com/new](https://vercel.com/new).  
   - Choisis **Import Git Repository** si le code est sur GitHub/GitLab, ou **Upload** pour envoyer un dossier.  
   - Si tu utilises Git : connecte le dépôt, puis continue.

3. **Configuration**  
   - **Root Directory** : laisse par défaut (ou le dossier qui contient `facial-harmony-analysis.html`).  
   - **Build Command** : laisse vide (pas de build).  
   - **Output Directory** : laisse vide ou `.`  
   - **Install Command** : laisse vide.

4. **Déploiement**  
   Clique sur **Deploy**. Vercel te donne une URL du type `https://ton-projet.vercel.app`.

5. **Page d’accueil**  
   Si ton site n’a qu’un seul fichier HTML à la racine, renomme-le en `index.html` pour qu’il soit servi par défaut, ou configure dans Vercel la **Redirect** : racine `/` → `/facial-harmony-analysis.html`.

   **Option simple** : dupliquer le fichier en `index.html` à la racine du projet pour que `https://ton-projet.vercel.app` affiche directement l’app.

---

## Netlify

1. Va sur [netlify.com](https://www.netlify.com) et crée un compte.  
2. **Add new site** → **Deploy manually** (ou connecte un dépôt Git).  
3. Glisse-dépose le dossier contenant `facial-harmony-analysis.html` (ou `index.html`).  
4. Netlify te donne une URL du type `https://xxx.netlify.app`.  
5. Pour que la racine ouvre l’app : nomme le fichier `index.html` ou configure **Redirects** dans **Site settings** → **Build & deploy** → **Redirects** :  
   `/*    /facial-harmony-analysis.html   200`

---

## GitHub Pages

1. Pousse le projet sur un dépôt GitHub.  
2. **Settings** → **Pages** → **Source** : **Deploy from a branch**.  
3. Choisis la branche (souvent `main`) et le dossier **/ (root)** ou **/docs** selon où se trouve ton HTML.  
4. Le site sera à `https://ton-username.github.io/ton-repo/`.  
5. Pour que la racine du site ouvre l’app : mets le fichier en `index.html` à la racine du dépôt (ou dans le dossier choisi pour Pages).

---

## Logo et fichier unique

- **Logo** : dans `facial-harmony-analysis.html`, définis `LOGO_URL = 'https://ton-site.com/logo.png'` (URL absolue) ou `LOGO_URL = '/logo.png'` si tu déploies `logo.png` à la racine du site.  
- **Un seul HTML** : tu peux ne déployer que `facial-harmony-analysis.html`. Pour que ce soit la page d’accueil sur Vercel/Netlify, renomme-le en `index.html` ou configure une redirection comme ci-dessus.

---

## Résumé

| Plateforme   | Gratuit | HTTPS | Domaine perso (optionnel) |
|-------------|--------|-------|----------------------------|
| Vercel      | Oui    | Oui   | Oui                        |
| Netlify     | Oui    | Oui   | Oui                        |
| GitHub Pages| Oui    | Oui   | Oui                        |

L’analyse tourne entièrement dans le navigateur (MediaPipe, Konva via CDN). Aucune donnée n’est envoyée à ton serveur : le site est prêt à être publié en l’état.
