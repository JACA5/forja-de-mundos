# Forja de Mundos

Herramienta para diseñar presentaciones narrativas interactivas de cursos: un tablero 16:9 con nodos navegables (personaje que "viaja" entre temas), con ayuda de Claude para ubicar nodos sobre una imagen de fondo y para generar el contenido a partir de un PDF o texto fuente.

Es un archivo estático (`index.html`) sin build ni dependencias de frontend. Las dos funciones de IA (analizar fondo, generar mundo) llaman a endpoints propios en `/api` que actúan de proxy hacia la API de Anthropic — la API key nunca se expone al navegador.

## Desarrollo local

Requiere la [Vercel CLI](https://vercel.com/docs/cli):

```bash
npm i -g vercel
vercel link      # una sola vez, vincula esta carpeta al proyecto forja-de-mundos
vercel env pull .env.local
vercel dev
```

`vercel dev` sirve `index.html` y las funciones de `/api` en `http://localhost:3000`.

## Variable de entorno

- `ANTHROPIC_API_KEY` — API key de Anthropic. Se configura en Vercel (Project Settings → Environment Variables) y se descarga localmente con `vercel env pull .env.local`. Ver `.env.example`.

## Deploy

```bash
vercel --prod
```

o hacer push a `main` si el proyecto tiene auto-deploy configurado en Vercel.

## Estructura

- `index.html` — toda la UI y lógica del editor/presentación.
- `api/analyze.js` — proxy para el análisis de imagen de fondo (ubicación de nodos + paleta).
- `api/generate.js` — proxy para la generación de mundo desde PDF/texto.

## Uso

1. **Mundo**: definir metáfora espacial, paleta, subir fondo (imagen/GIF/video) y personaje.
2. **Nodos**: agregar nodos manualmente o dejar que la IA los ubique sobre el fondo (🔍).
3. **⚡ IA**: adjuntar un PDF o pegar texto fuente y generar el mundo completo (escenas, nodos, contenido).
4. **Presentar**: modo fullscreen navegable; **Exportar HTML** genera un archivo standalone con todo incluido (imágenes/video en base64).
