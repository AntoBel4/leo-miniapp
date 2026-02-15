# Léo OS — Telegram Web Mini App

Mini application Telegram (Web Mini App) pour **Léo** : un dashboard “whaouh” avec modules **Admin / Projets / Contenu / Coach**.

## 1) Ce que c’est
- Une page web statique (`index.html`) affichée *dans Telegram* via les options **Telegram Mini Apps** (BotFather).
- Elle détecte le module à ouvrir via le paramètre Telegram :
  - `Telegram.WebApp.initDataUnsafe.start_param`
  - et en fallback `?tgWebAppStartParam=...`

## 2) Modules (start_param)
- `today` : Dashboard “Aujourd’hui”
- `admin` : Administration
- `projects` : Projets / Workflows
- `content` : Contenu / SEO
- `coach` : Coach sport & perte de poids

> Exemples : ouvrir directement un module depuis Telegram
- `... startapp=today`
- `... startapp=coach`
- `... startapp=projects`

## 3) Communication avec le bot (OpenClaw)
L’UI envoie une action au bot via :
- `Telegram.WebApp.sendData(JSON.stringify({ action, payload }))`

Le bot doit :
1) recevoir la donnée
2) déclencher le bon skill OpenClaw
3) répondre dans le chat Telegram

⚠️ Aucun secret / token ne doit être dans le front (`index.html`).

## 4) Développement local
Ouvre simplement `index.html` dans un navigateur.

Hors Telegram, les boutons affichent un debug (console + alert).
Dans Telegram, ils enverront les actions via `sendData`.

## 5) Déploiement (Vercel recommandé)
1. Va sur https://vercel.com/new
2. **Import Git Repository** → sélectionne `AntoBel4/leo-miniapp`
3. Framework : **Other**
4. Build command : *(vide)*
5. Output directory : *(vide)*
6. Deploy

Tu obtiens une URL du style :
`https://leo-miniapp-xxxxx.vercel.app`

C’est cette URL qu’il faut mettre dans BotFather / Telegram Mini Apps.

## 6) Configuration Telegram (BotFather)
### A) Menu Button (option “Mini Apps”)
- Title : `📋 Menu`
- URL : `https://TON_URL_VERCEL`

### B) Lancer un module directement (startapp)
Quand tu crées des liens “Direct Links” dans BotFather, tu peux utiliser l’ouverture par module.
L’idée :
- un direct link = un module

## 7) Roadmap (version 1 → version 2)
### V1 (déjà faite)
- UI “whaouh” + modules + envoi d’actions au bot

### V2
- Connecter réellement Notion & Google Calendar côté OpenClaw (réponse dans le chat)
- Ajouter une page “Historique / Logs”
- Ajouter une page “Paramètres”

## 8) Sécurité
- Tout ce qui écrit dans Notion / Calendar doit demander une validation explicite (“ok”).
- Le front ne fait que demander des actions ; le backend (bot/OpenClaw) décide.
