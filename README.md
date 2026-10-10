# Greeting App

Aplicación FastAPI que recibe un nombre y un apellido y devuelve un saludo personalizado.

Este repositorio hace parte de un **laboratorio guiado del curso Fundamentos de DevOps y SRE** (Universidad Nacional de Colombia). El objetivo es practicar integración y despliegue continuo (CI/CD): análisis estático, pruebas automatizadas, construcción de imágenes de contenedor y despliegue en AWS.

La guía completa del laboratorio está en [docs/lab1.md](docs/lab1.md).

## Requisitos

- Python 3.12
- [Poetry](https://python-poetry.org/)
- Docker 

## Ejecución local

```bash
poetry install
poetry run uvicorn main:app --app-dir src --reload
```

La documentación interactiva de la API queda disponible en `http://localhost:8000/docs`.

## Calidad y pruebas

```bash
poetry run pylint src
poetry run pytest tests -vv
```

## Pipeline de CI/CD

El flujo de GitHub Actions (`.github/workflows/`) ejecuta:

1. **Lint**: análisis estático con Pylint.
2. **Pruebas**: pruebas unitarias con Pytest.
3. **Build & Push**: construcción de la imagen Docker y publicación en Amazon ECR.
4. **Deploy**: despliegue en Amazon ECS sobre EC2 mediante `scripts/deploy.sh`.

Los pasos 3 y 4 solo se ejecutan con un push a `main` o al lanzar el flujo manualmente.