# OpenShift Platform Security Playground

Laboratorio personal de Platform Security sobre OpenShift Local (CRC), construido con enfoque GitOps y orientado a automatización, seguridad y operación de plataforma.

La idea es gestionar tanto aplicaciones como infraestructura desde Git, manteniendo el entorno lo más autocontenido posible dentro del cluster y usando únicamente herramientas open source o incluidas en el ecosistema OpenShift, sin dependencias de licencias comerciales adicionales.

## Objetivo

Construir una plataforma reproducible que permita experimentar con:

- CI con Tekton
- CD/GitOps con Argo CD
- políticas de seguridad con Kyverno
- detección de amenazas en runtime con Falco
- escaneo de imágenes con Trivy
- gestión de certificados con cert-manager
- gestión de secretos con External Secrets
- autenticación con Keycloak
- observabilidad con Prometheus y Grafana
- alertado por correo mediante un servidor SMTP interno
- backup y recuperación con OADP

## Arquitectura

### Externo

Solo se usan servicios externos cuando tiene sentido:

- GitHub → código fuente y manifiestos GitOps
- Quay → registro de imágenes

### Dentro del cluster

Todo lo demás vive dentro de OpenShift:

- OpenShift GitOps (Argo CD)
- OpenShift Pipelines (Tekton)
- Kyverno
- Falco
- Trivy
- cert-manager
- External Secrets
- Keycloak
- Prometheus
- Grafana
- servidor SMTP interno
- OADP
- aplicaciones de prueba

## Flujo

1. Se hace push a GitHub
2. Tekton ejecuta CI (build, test, escaneo, push a Quay)
3. Argo CD detecta cambios y sincroniza
4. OpenShift aplica el estado deseado
5. Kyverno valida políticas
6. Falco monitoriza runtime
7. Prometheus recoge métricas
8. Grafana visualiza dashboards
9. Alertmanager envía alertas vía SMTP interno

## Estructura

```text
argocd/          Configuración GitOps y App of Apps
bootstrap/       Recursos iniciales del cluster
operators/       Instalación de operadores
platform/        Servicios base de plataforma
security/        Políticas y controles de seguridad
observability/   Métricas, alertas y dashboards
pipelines/       CI con Tekton
applications/    Aplicaciones de prueba
docs/            Documentación y notas
scripts/         Utilidades auxiliares