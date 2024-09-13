# Icebreaker

## Developing

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Container

```
docker run --rm -it -v "$(pwd):/app" -w /app -p 80:5173 node:18 bash
```