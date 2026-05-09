# OpenShift Platform Security Playground

Laboratorio local de Platform Security sobre OpenShift Local / CRC.

Este proyecto tiene como objetivo construir una plataforma de seguridad, observabilidad y automatización basada en GitOps, manteniendo la mayor parte de los componentes dentro del cluster OpenShift y usando servicios externos solo cuando aportan valor claro, como GitHub para el código fuente y Quay como registro de imágenes externo.

## Objetivos

- Gestionar aplicaciones e infraestructura usando GitOps con Argo CD.
- Construir imágenes mediante pipelines Tekton.
- Publicar imágenes en Quay externo.
- Aplicar políticas de seguridad con Kyverno.
- Detectar amenazas en runtime con Falco.
- Escanear vulnerabilidades de imágenes con Trivy.
- Gestionar certificados con cert-manager.
- Gestionar secretos mediante External Secrets.
- Añadir visibilidad de red con OpenShift Network Observability.
- Centralizar métricas y dashboards con Prometheus y Grafana.
- Enviar alertas a un servidor SMTP desplegado dentro del cluster.

## Arquitectura general

El entorno se ejecuta sobre un cluster OpenShift Local / CRC.

Los únicos elementos externos principales son:

- GitHub, como repositorio de código y manifiestos GitOps.
- Quay, como registro externo de imágenes.

Dentro del cluster se despliegan los componentes de CI/CD, seguridad, observabilidad, autenticación, certificados, secretos, alertas y aplicaciones de ejemplo.

## Flujo general

1. Los desarrolladores hacen push de código y manifiestos a GitHub.
2. Tekton ejecuta pipelines de CI para construir, probar y escanear imágenes.
3. Las imágenes se publican en Quay.
4. Argo CD detecta cambios en Git y sincroniza el estado deseado.
5. OpenShift despliega aplicaciones, infraestructura y configuración de seguridad.
6. Kyverno valida políticas de seguridad.
7. Falco detecta comportamiento sospechoso en runtime.
8. Trivy analiza vulnerabilidades de imágenes.
9. Network Observability aporta visibilidad de flujos de red.
10. Prometheus y Grafana permiten monitorización y dashboards.
11. Las alertas se envían a un servidor SMTP interno del cluster.

## Estructura del repositorio

```text
argocd/          Manifiestos de Argo CD y patrón App of Apps.
bootstrap/       Recursos iniciales necesarios antes de GitOps.
operators/       Instalación declarativa de operadores.
platform/        Configuración base de plataforma.
security/        Políticas, runtime security, RBAC y escaneo.
observability/   Métricas, dashboards, tracing y red.
applications/    Aplicaciones demo.
pipelines/       Pipelines Tekton.
docs/            Documentación del proyecto.
scripts/         Scripts auxiliares.