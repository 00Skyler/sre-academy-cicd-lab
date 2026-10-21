# Plantillas iniciales de GitHub Actions (principiantes)

Estas plantillas **no son las soluciones**. Sirven para completar los pasos `TODO` de dos workflows en el repositorio de laboratorio.

## Antes de empezar

1. Haz un **fork** de https://github.com/aromero15/sre-academy o usa el repositorio de laboratorio indicado por el instructor.
2. Asegúrate de que la aplicación está en la **raíz** del fork: `requirements.txt`, `scripts/test.sh`, `Dockerfile`, `app.py`, `services/` y `tests/`.
3. Crea una rama `feature/ci-training` desde `main`.
4. Si ya existe `.github/workflows/ci.yml`, edítalo en tu fork: no crees dos archivos `ci.yml` con el mismo propósito.

## Actividad A: validar Pull Requests

1. Copia `plantillas/pr.yml` a `.github/workflows/pr.yml` **en tu rama feature**.
2. Completa `TODO 1`: instala las dependencias desde `requirements.txt`.
3. Completa `TODO 2`: ejecuta todas las pruebas usando `scripts/test.sh`.
4. **Elimina ambos `exit 1`** cuando hayas reemplazado las instrucciones TODO.
5. Commit y push a `feature/ci-training`.
6. Abre un PR **desde tu rama hacia main de tu propio fork**. Revisa **Checks**.
7. Como prueba de fallo, cambia temporalmente en `tests/test_tasks.py` la expectativa del status HTTP de `200` a `500`, haz push y revisa los logs. Luego restaura `200` y haz otro push.

## Actividad B: CI/CD al integrar a main

1. Copia `plantillas/ci.yml` a `.github/workflows/ci.yml` **en la misma rama feature**.
2. Completa `TODO 1` y `TODO 2`: instala dependencias y ejecuta `bash scripts/test.sh`.
3. Completa `TODO 3`: construye una imagen con `docker build` (el runner de Ubuntu tiene Docker disponible).
4. Completa `TODO 4` y `TODO 5`: usa `echo` para **simular** staging y producción.
5. **Elimina todos los `exit 1`** cuando reemplaces los TODO.
6. Commit y push. Espera a que el PR tenga las pruebas en verde. Haz merge a `main` de tu fork.
7. Abre **Actions** y revisa el flujo `test → build → deploy-staging → deploy-production`.

## Pistas

| Objetivo | Comando útil |
| --- | --- |
| Instalar dependencias | `python -m pip install -r requirements.txt` |
| Ejecutar pruebas | `bash scripts/test.sh` |
| Construir imagen | `docker build -t sre-academy-app:training .` |
| Imprimir mensaje | `echo "Deploy simulado"` |

**Recuerda:** `needs` hace que un job espere a otro y no continúe si falló. Los jobs staging y production son simulaciones; no despliegan nada real. Si ya tienes un workflow heredado del fork, puede producir ejecuciones adicionales hasta que lo edites o desactives.
