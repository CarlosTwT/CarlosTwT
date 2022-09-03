# How to get refresh_token from Spotify API

- Primero ve a [developer.spotify.com](https://developer.spotify.com/)'s tablero
- Obtener ID de cliente y Secreto de cliente de una página
- Agregar `http://localhost/callback` en Editar configuración en el panel
- Pon esta URL

```
https://accounts.spotify.com/authorize?client_id={SPOTIFY_CLIENT_ID}&response_type=code&scope=user-read-currently-playing,user-read-recently-played&redirect_uri=http://localhost/callback/
```

en el navegador, obtendrá URL algo así como `http://localhost/callback/?code={CODE}`

- Luego, tome la codificación Base64 de `{SPOTIFY_CLIENT_ID}:{SPOTIFY_CLIENT_SECRET}` and `{CODE}` para solicitar token de actualización usando:

```sh
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Authorization: Basic {ENCODE}" -d "grant_type=authorization_code&redirect_uri=http://localhost/callback/&code={CODE}" https://accounts.spotify.com/api/token
```

- Ahora, podemos poner

```sh
SPOTIFY_CLIENT_ID='____'
SPOTIFY_SECRET_ID='____'
SPOTIFY_REFRESH_TOKEN='____'
```

into `.env` file for development

- Run `python spotify-playing.py` to server via `http://localhost:5000`

# Deployment
- Usar la función sin servidor de Vercel https://vercel.com/docs/v2/serverless-functions/introduction

Original document by @titipata
