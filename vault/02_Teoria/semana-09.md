---
semana: 9
tema: AWS — cuenta, IAM y consola
estado: pendiente
---

# Semana 9 — AWS: cuenta, IAM y la consola

> Tiempo estimado: 3–4 horas (mas lectura que codigo)
> Al terminar: `bash scripts/push.sh "semana-09 aws-iam"`

---

## ¿Que es AWS?

Amazon Web Services (AWS) es la plataforma de computacion en la nube mas grande del mundo. En lugar de tener un servidor fisico, rentas recursos computacionales de Amazon que pagan solo lo que usas.

Carlos usa AWS en INE/PREP para:
- Lambda (codigo que corre sin servidor)
- S3 (almacenamiento de archivos)
- API Gateway (exponer APIs a internet)
- ElastiCache/Redis (cache)
- MySQL en RDS

---

## Crear cuenta AWS (Free Tier)

1. Ve a: https://aws.amazon.com
2. Crea una cuenta — necesitas tarjeta de credito/debito
3. El **Free Tier** te da 12 meses de uso gratuito limitado:
   - Lambda: 1 millon de invocaciones gratis/mes
   - S3: 5 GB gratis
   - EC2: 750 horas de t2.micro gratis
4. **Importante:** configura alertas de billing para no recibir cargos inesperados:
   - Billing Dashboard → Billing Preferences → Receive Free Tier Usage Alerts

---

## IAM — Identidad y Acceso

**IAM** (Identity and Access Management) controla QUIEN puede hacer QUE en tu cuenta AWS.

Conceptos clave:
- **Root user:** la cuenta principal — solo usarla para crear el primer admin
- **IAM User:** usuario con permisos especificos — usar siempre en lugar del root
- **Role:** conjunto de permisos que se le asigna a un servicio (ej: Lambda puede leer S3)
- **Policy:** documento JSON que define los permisos

### Crear tu primer usuario IAM

1. Consola AWS → IAM → Users → Create User
2. Nombre: `jess-dev`
3. Permisos: adjuntar policy `AdministratorAccess` (para aprender — en produccion seria mas restrictivo)
4. Crear Access Key para uso desde CLI

---

## AWS CLI — controlar AWS desde la terminal

```bash
# Instalar AWS CLI
pip install awscli

# Configurar con tus credenciales
aws configure
# AWS Access Key ID: tu-access-key
# AWS Secret Access Key: tu-secret-key
# Default region name: us-east-1
# Default output format: json

# Verificar que funciona
aws sts get-caller-identity
```

---

## Servicios principales (resumen)

| Servicio | Para que | Lo usaremos |
|---------|----------|-------------|
| Lambda | Codigo sin servidor | Semana 10-12 |
| S3 | Almacenamiento de archivos | Semana 11 |
| API Gateway | Exponer endpoints HTTP | Semana 12 |
| IAM | Permisos y usuarios | Esta semana |
| DynamoDB | BD NoSQL serverless | Semana 12 |
| CloudWatch | Logs y monitoreo | Siempre |

---

## A recordar

- Nunca usar el root user para tareas cotidianas — crea siempre un IAM user
- Free Tier = gratis con limites por 12 meses
- Configura alertas de billing ANTES de crear cualquier recurso
- AWS CLI permite controlar todo desde la terminal

---

[[03_Practicas/semana-09]]
