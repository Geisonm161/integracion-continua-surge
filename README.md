# Integración continua con GitHub Actions y Surge.sh

Proyecto del primer parcial: una página web estática desplegada automáticamente en
[Surge.sh](https://surge.sh/) después de cada `push` a la rama `main`.

- **Sitio publicado:** <https://geisonm161-ci-lab.surge.sh>
- **Repositorio:** <https://github.com/Geisonm161/integracion-continua-surge>

## Flujo de despliegue

1. GitHub recibe un cambio en `main`.
2. El workflow `.github/workflows/main.yml` descarga el repositorio.
3. GitHub Actions instala la CLI de Surge.
4. Surge publica la página usando secretos protegidos.

## Configuración inicial

### 1. Instalar Surge y obtener el token

```bash
npm install --global surge
surge login
surge token
```

Guarda el token mostrado; no lo agregues al código ni al historial de Git.

### 2. Reservar o elegir el dominio

El dominio configurado para este proyecto es `geisonm161-ci-lab.surge.sh`. El primer
despliegue local permite confirmar que está disponible:

```bash
surge . geisonm161-ci-lab.surge.sh
```

### 3. Crear los secretos en GitHub

En el repositorio, abre **Settings → Secrets and variables → Actions → New repository secret**
y crea:

| Secreto | Valor |
| --- | --- |
| `SURGE_TOKEN` | Token obtenido con `surge token` |
| `SURGE_DOMAIN` | `geisonm161-ci-lab.surge.sh` |

### 4. Activar el despliegue

```bash
git push origin main
```

El progreso puede verificarse en la pestaña **Actions** del repositorio.

## Desarrollo local

La página no necesita compilación ni dependencias. Puede abrirse directamente desde
`index.html` o servirse con cualquier servidor HTTP local.

## Seguridad

Las credenciales de Surge se consumen únicamente desde GitHub Actions mediante
`secrets`. Nunca deben guardarse en archivos del repositorio.
