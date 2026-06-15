# Docker — PostgreSQL local para practicas

Necesitas Docker a partir de la Semana 8 (FastAPI + PostgreSQL).

## Instalar Docker Desktop

**Windows / macOS:** Descarga desde docker.com/products/docker-desktop

**Linux (Ubuntu):**
```bash
sudo apt update
sudo apt install docker.io docker-compose
sudo systemctl start docker
sudo usermod -aG docker $USER  # para no usar sudo siempre
```

---

## Levantar PostgreSQL para el curso

```bash
docker run -d \
  --name jess-postgres \
  -e POSTGRES_USER=alumno \
  -e POSTGRES_PASSWORD=alumno123 \
  -e POSTGRES_DB=mi_escuela \
  -p 5432:5432 \
  -v jess-postgres-data:/var/lib/postgresql/data \
  postgres:16
```

## Comandos utiles

```bash
# Ver contenedores corriendo
docker ps

# Iniciar contenedor ya creado
docker start jess-postgres

# Detener
docker stop jess-postgres

# Ver logs
docker logs jess-postgres

# Conectarse a la BD desde terminal
docker exec -it jess-postgres psql -U alumno -d mi_escuela
```

---

## Conectar desde Python (semana 8)

```python
DATABASE_URL = "postgresql://alumno:alumno123@localhost:5432/mi_escuela"
```

---

## DBeaver — ver la BD visualmente (opcional)

1. Descarga DBeaver desde dbeaver.io
2. New Connection → PostgreSQL
3. Host: `localhost`, Port: `5432`
4. User: `alumno`, Password: `alumno123`
5. Database: `mi_escuela`
