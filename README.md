# Adivina el Número — API (FastAPI)

Pequeña API en memoria que mantiene un número secreto. Endpoints:

- `POST /start` o `/comenzar` — inicia un nuevo juego (cuerpo JSON: `min`, `max`).
- `GET /guess?number=XX` o `/adivinar?numero=XX` — realiza un intento; devuelve `alto`, `bajo` o `correcto`.
- `GET /status` o `/estado` — devuelve estado del juego; `reveal=true` o `reveal=true` muestra el secreto.

Requisitos
- Python 3.9+

Instalación local (PowerShell):

```powershell
python -m venv .venv
# Si no puedes ejecutar Activate.ps1 por políticas de ejecución, usa los ejecutables del venv directamente.
# Para activar (si está permitido):
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
uvicorn adivina:app --reload --port 8000
```

Probar endpoints (PowerShell) — usar `Invoke-RestMethod`:

- Iniciar juego (ejemplo):

```powershell
Invoke-RestMethod -Uri "http://127.0.0.1:8000/start" -Method Post `
  -Headers @{ 'Content-Type' = 'application/json' } `
  -Body '{"min":1,"max":50}'
```

O en español:

```powershell
Invoke-RestMethod -Uri "http://127.0.0.1:8000/comenzar" -Method Post `
  -Headers @{ 'Content-Type' = 'application/json' } `
  -Body '{"min":1,"max":50}'
```

- Intentar adivinar (ejemplo):

```powershell
Invoke-RestMethod -Uri "http://127.0.0.1:8000/guess?number=25" -Method Get
```

O en español:

```powershell
Invoke-RestMethod -Uri "http://127.0.0.1:8000/adivinar?numero=25" -Method Get
```

- Ver estado (sin revelar):

```powershell
Invoke-RestMethod -Uri "http://127.0.0.1:8000/status" -Method Get
```

- Ver estado y revelar secreto (solo debugging):

```powershell
Invoke-RestMethod -Uri "http://127.0.0.1:8000/estado?reveal=true" -Method Get
```

Si prefieres la sintaxis clásica `curl`, usa `curl.exe` en PowerShell:

```powershell
curl.exe -X POST "http://127.0.0.1:8000/start" -H "Content-Type: application/json" -d '{"min":1,"max":50}'
```

Docker (build y run):

```powershell
docker build -t adivina-api:latest .
docker run -p 8000:8000 adivina-api:latest
```

Despliegue en la nube (resumen):
- Subir imagen a Docker Hub / Container Registry y desplegar en el servicio que prefieras (Azure App Service, AWS ECS, Render, Fly, etc.).
# Adivina el Número — API (FastAPI)

Pequeña API en memoria que mantiene un número secreto. Endpoints:

- `POST /start` — inicia un nuevo juego (cuerpo JSON: `min`, `max`).
- `GET /guess?number=XX` — realiza un intento; devuelve `alto`, `bajo` o `correcto`.
- `GET /status` — devuelve estado del juego; `reveal=true` muestra el secreto.

Requisitos
- Python 3.9+

Instalación local (PowerShell):

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
uvicorn adivina:app --reload --port 8000
```

Probar endpoints
- Inicia juego (opcional min/max):

```powershell
curl -X POST "http://127.0.0.1:8000/start" -H "Content-Type: application/json" -d '{"min":1,"max":50}'
```

- Intentar adivinar:

```powershell
curl "http://127.0.0.1:8000/guess?number=25"
```

Docker (build y run):

```powershell
docker build -t adivina-api:latest .
docker run -p 8000:8000 adivina-api:latest
```

Despliegue en la nube (resumen):
- Subir imagen a Docker Hub / Container Registry y desplegar en el servicio que prefieras (Azure App Service, AWS ECS, Render, Fly, etc.).
