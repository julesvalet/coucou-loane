# Brancher le bloc-note partagé (Firebase) 💞

Le code est déjà prêt : il ne manque que **tes clés**. 5 minutes, tout est gratuit.

## 1. Créer le projet

1. Va sur https://console.firebase.google.com et connecte-toi avec ton compte Google
2. **Créer un projet** → nom : `coucou-loane` → tu peux désactiver Google Analytics → Créer

## 2. Créer la base de données

1. Dans le menu de gauche : **Créer** → **Realtime Database**
2. **Créer une base de données**
3. Emplacement : **europe-west1** (Belgique, le plus proche)
4. Choisis **Démarrer en mode verrouillé** (on met les bonnes règles juste après)

## 3. Coller les règles de sécurité

Onglet **Règles** de la Realtime Database, remplace tout par ceci puis **Publier** :

```json
{
  "rules": {
    "couples": {
      "$code": {
        ".read": "$code.length >= 8",
        ".write": "$code.length >= 8"
      }
    }
  }
}
```

Ces règles font que personne ne peut lister les couples : il faut connaître votre code secret exact pour accéder à vos pages.

## 4. Récupérer la config

1. ⚙️ **Paramètres du projet** (en haut à gauche)
2. Tout en bas, section **Vos applications** → clique sur l'icône **Web `</>`**
3. Nom de l'app : `coucou-loane` → **Enregistrer l'application**
4. Firebase affiche un bloc `const firebaseConfig = { ... }`

## 5. Coller dans `config.js`

Ouvre le fichier `config.js` et recopie les valeurs :

```js
window.FIREBASE_CONFIG = {
  apiKey: "AIza...",
  authDomain: "coucou-loane.firebaseapp.com",
  databaseURL: "https://coucou-loane-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "coucou-loane",
  appId: "1:123...:web:abc..."
};
```

⚠️ Le `databaseURL` est le plus important. S'il n'apparaît pas dans le bloc affiché par Firebase, copie-le depuis la page **Realtime Database** (c'est l'adresse affichée en haut).

Puis publie :

```bash
cd "C:\Users\jules\Documents\duoweb" && git add -A && git commit -m "Config Firebase" && git push
```

## 6. Le code secret du couple

À la première ouverture du bloc-note, le site demande un **code secret**.
Mettez **exactement le même** sur les deux téléphones (au moins 8 caractères), par exemple `loloetjuju29092022`.

C'est ce code qui relie vos deux téléphones.

## Ce qu'il faut savoir 🔐

- Les pages **🔒 privées** ne partent **jamais** en ligne : elles restent sur le téléphone de celui qui les écrit.
- Les pages **💞 partagées** sont dans Firebase. Quiconque connaît votre code secret pourrait les lire → choisissez un code que personne ne devine, et ne le donnez à personne.
- Si `config.js` reste vide, tout continue de marcher, mais chaque téléphone garde ses propres pages.
