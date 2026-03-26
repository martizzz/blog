# Blog personal en GitHub Pages + Firebase

## Archivos incluidos

- `index.html`: la web del blog.
- `firebase-config.example.js`: ejemplo de configuración de Firebase.
- `firestore.rules`: reglas de Firestore.
- `storage.rules`: reglas de Firebase Storage.
- `firebase.json`: configuración para desplegar reglas con Firebase CLI.

## 1. Crear proyecto en Firebase

1. Entra en Firebase Console.
2. Crea un proyecto nuevo.
3. Activa **Firestore Database** en modo producción o pruebas.
4. Activa **Firebase Storage**.
5. En `Configuración del proyecto > Tus aplicaciones`, crea una app web.
6. Copia la configuración y pégala en un nuevo archivo llamado `firebase-config.js` usando `firebase-config.example.js` como plantilla.

## 2. Crear firebase-config.js

Crea un archivo llamado `firebase-config.js` en la misma carpeta que `index.html`.

Ejemplo:

```js
export const firebaseConfig = {
  apiKey: 'TU_API_KEY',
  authDomain: 'TU_PROYECTO.firebaseapp.com',
  projectId: 'TU_PROYECTO',
  storageBucket: 'TU_PROYECTO.firebasestorage.app',
  messagingSenderId: '1234567890',
  appId: '1:1234567890:web:abcdefghijk'
};

export const ADMIN_PASSWORD = 'TU_PASSWORD';
export const COLLECTION_NAME = 'posts';
```

## 3. Reglas

Estas reglas son abiertas para que el prototipo funcione rápido. Eso significa que cualquiera podría escribir en la base de datos si descubre los endpoints. Para una versión real, conviene usar Firebase Authentication y restringir escritura solo a usuarios autenticados.

## 4. Subir a GitHub Pages

1. Sube `index.html` y `firebase-config.js` a tu repositorio.
2. Ve a `Settings > Pages`.
3. Selecciona la rama principal y la carpeta raíz.
4. Guarda.
5. Tu web quedará publicada en la URL de GitHub Pages.

## 5. Publicar reglas con Firebase CLI

Instala Firebase CLI:

```bash
npm install -g firebase-tools
```

Haz login:

```bash
firebase login
```

Inicializa o usa tu proyecto:

```bash
firebase use --add
```

Sube reglas:

```bash
firebase deploy --only firestore:rules,storage
```

## 6. Estructura de un post en Firestore

Cada documento en la colección `posts` guarda:

```json
{
  "title": "Título opcional",
  "author": "admin",
  "text": "Texto del post",
  "images": ["https://..."],
  "links": [
    {
      "url": "https://...",
      "label": "Texto del enlace"
    }
  ],
  "createdAt": "serverTimestamp()"
}
```

## 7. Importante sobre seguridad

La contraseña del archivo `firebase-config.js` solo oculta el panel en el navegador. No protege de verdad Firestore ni Storage. Para una versión segura, hay que usar autenticación real y reglas privadas.
