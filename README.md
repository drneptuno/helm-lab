🧾 Documento: Automatización del Despliegue con ArgoCD y Helm sobre Kubernetes local

✅ Objetivo del proceso
Automatizar completamente el paso del cambio de imagen a la ejecución del despliegue, eliminando pasos manuales innecesarios, asegurando trazabilidad y reduciendo riesgos humanos.

🔹 Solución Implementada
Se implementó un entorno GitOps utilizando ArgoCD y Helm, junto con un cluster de desarrollo en Minikube para pruebas locales.

🔧 Pasos realizados:
Preparación del entorno local:

Instalación de Minikube y despliegue de ArgoCD en el namespace argocd.

Repositorio Git:

    Se creó un repositorio Git con una estructura Helm (charts/servicio) y archivos values.yaml con el tag de imagen versionado.

Creación de aplicación en ArgoCD:

    Se definió la app servicio que apunta al repositorio Git.

    Se habilitó sincronización automática con políticas de:

    auto-sync: aplicar cambios sin intervención.

    prune: eliminar recursos obsoletos.

    self-heal: reponer recursos modificados fuera de Git.

Prueba de despliegue automático:

    Se actualizó el tag de imagen en values.yaml, se hizo commit y push.

    ArgoCD detectó el cambio, desplegó la nueva versión en Kubernetes, y eliminó los recursos antiguos automáticamente.

🔍 Beneficios Obtenidos

| Aspecto                | Antes                                      | Después (Automatizado)                               |
| ---------------------- | ------------------------------------------ | ---------------------------------------------------- |
| Despliegue             | Manual con `helm upgrade`                  | Automático vía ArgoCD al detectar cambios en Git     |
| Tiempo de intervención | Alto (edición manual + comandos)           | Nulo o muy bajo (solo revisión si es necesario)      |
| Trazabilidad           | Parcial (sin seguimiento claro de cambios) | Completa (todo versionado en Git, visible en ArgoCD) |
| Riesgo de error humano | Alto                                       | Bajo                                                 |
| Rollbacks              | Manual, propenso a errores                 | ArgoCD permite `rollback` automático desde la UI     |
| Visibilidad del estado | Indirecta (requiere acceso a pods)         | Directa desde UI web de ArgoCD                       |

👤 Nuevo Rol en el Proceso

    Antes, tu rol implicaba intervención operativa manual en cada despliegue.

    Ahora, tu función se transforma en un rol de supervisión y control de calidad, enfocado en:

    Monitorear el estado de las aplicaciones vía ArgoCD.

    Validar y aprobar cambios críticos (si se configura validación manual).

    Gestionar incidentes o rollbacks si se presentan fallos.

    Administrar la configuración general del entorno GitOps.

    Documentar y extender el proceso a otros servicios y equipos.

    Este cambio te posiciona como operador de plataforma, más que como ejecutor manual de despliegues.

🧪 Laboratorio local

    Se implementó un entorno de pruebas usando Minikube, el cual replica en forma controlada el flujo de despliegue y permite:

    Validar comportamiento de ArgoCD.

    Testear cambios antes de aplicarlos en entornos productivos.

    Capacitar equipos de desarrollo en el flujo GitOps.