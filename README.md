# Cours complet sur `fetch` en JavaScript

## Introduction à `fetch`

`fetch` est une API native de JavaScript qui permet de faire des requêtes HTTP (GET, POST, etc.) pour interagir avec des serveurs (API REST, fichiers distants, etc.).

---

## Syntaxe de base

```js
fetch(url)
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Erreur :', error));
```

### Exemple simple :

```js
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(res => res.json())
  .then(post => console.log(post));
```

---

## Faire une requête POST

```js
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    title: 'Hello',
    body: 'World',
    userId: 1
  })
})
.then(res => res.json())
.then(data => console.log(data));
```

---

## Méthodes HTTP disponibles

* `GET` : Lire une ressource
* `POST` : Créer une ressource
* `PUT` : Remplacer une ressource
* `PATCH` : Modifier une partie d'une ressource
* `DELETE` : Supprimer une ressource

---

## Vérification des erreurs manuellement

```js
fetch('https://jsonplaceholder.typicode.com/posts/12345')
  .then(res => {
    if (!res.ok) throw new Error('Erreur HTTP : ' + res.status);
    return res.json();
  })
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

---

## Utiliser `async/await`

```js
async function getPost(id) {
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/posts/${id}`);
    if (!response.ok) throw new Error('Erreur : ' + response.status);
    const data = await response.json();
    console.log(data);
  } catch (err) {
    console.error(err);
  }
}

getPost(1);
```

---

## Envoyer des formulaires

```js
const formData = new FormData();
formData.append('username', 'john');
formData.append('avatar', fileInput.files[0]);

fetch('/upload', {
  method: 'POST',
  body: formData
});
```

---

## Headers personnalisés

```js
fetch('/api/data', {
  headers: {
    'Authorization': 'Bearer token_ici',
    'X-Custom-Header': 'MaValeur'
  }
});
```

---
