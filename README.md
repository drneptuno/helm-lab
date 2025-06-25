# 🚀 Automatización del Despliegue con ArgoCD y Helm sobre Kubernetes (Minikube)

Este laboratorio documenta la implementación de un entorno **GitOps** automatizado utilizando **ArgoCD**, **Helm** y **Kubernetes (Minikube)**. Su propósito es eliminar pasos manuales en el proceso de despliegue, mejorando la trazabilidad, velocidad y seguridad del pipeline.

---

## ✅ Objetivo

> Automatizar completamente el paso desde el cambio de versión de una imagen hasta su despliegue en Kubernetes, eliminando la intervención manual innecesaria y reduciendo el riesgo de errores humanos.

---

## 🧩 Arquitectura y Solución Implementada

Se construyó un flujo de automatización utilizando las siguientes herramientas:

- ✅ **Minikube** como entorno de Kubernetes local.
- ✅ **ArgoCD** para la gestión GitOps.
- ✅ **Helm** para empaquetado y despliegue de aplicaciones.
- ✅ **GitHub** como fuente de la verdad para el código y configuración.

---

## 🔧 Pasos Realizados

### 1. Preparación del Entorno Local

- Instalación de **Minikube**.
- Despliegue de **ArgoCD** en el namespace `argocd`.
- Acceso a la interfaz de ArgoCD.

### 2. Estructura del Repositorio Git

- Se creó un repositorio con estructura Helm:

helm-lab/
└── charts/
└── servicio/
├── Chart.yaml
├── values.yaml
└── templates/

- El archivo `values.yaml` contiene el tag de imagen versionado.

### 3. Creación de la Aplicación en ArgoCD

- Se definió la app `servicio` en ArgoCD apuntando al repo Git.
- Se habilitaron políticas:
- 🔁 `auto-sync`: sincroniza cambios automáticamente.
- 🧹 `prune`: elimina recursos obsoletos.
- 🛠️ `self-heal`: repara recursos modificados fuera de Git.

### 4. Prueba del Despliegue Automático

- Se actualizó el tag de imagen en `values.yaml`, commit y push.
- ArgoCD detectó el cambio automáticamente y desplegó la nueva versión.
- Los recursos obsoletos fueron eliminados sin intervención manual.

---

## 📈 Comparativa: Antes vs Después

| Aspecto                  | Antes (Manual)                      | Después (Automatizado con ArgoCD)        |
|--------------------------|-------------------------------------|------------------------------------------|
| **Despliegue**           | `helm upgrade` manual               | Git push → ArgoCD → despliegue automático |
| **Tiempo de intervención** | Alto                              | Bajo o nulo                               |
| **Trazabilidad**         | Parcial                             | Completa en Git y visible en ArgoCD       |
| **Errores humanos**      | Frecuentes                          | Minimizado                                |
| **Rollbacks**            | Manual, propenso a errores          | Con un clic desde la UI de ArgoCD         |
| **Visibilidad del estado** | Requiere inspección manual         | Panel visual desde la UI de ArgoCD        |

---

## 👤 Rol Actualizado del Operador

**Antes**: Intervención operativa directa en cada despliegue.  
**Ahora**: Rol orientado a plataforma, control de calidad y supervisión.

Nuevas responsabilidades:

- 👀 Monitorear aplicaciones desde ArgoCD.
- ✅ Validar cambios críticos si se requiere aprobación manual.
- 🚑 Gestionar incidentes y ejecutar rollbacks.
- 🧰 Administrar configuración GitOps y mantener el repositorio.
- 📚 Documentar y escalar el modelo a nuevos servicios/equipos.

---

## 🧪 Laboratorio Local

> Se armó un laboratorio de pruebas en Minikube que replica el flujo productivo en un entorno controlado.

Beneficios del laboratorio:

- Simular y validar despliegues sin afectar ambientes reales.
- Capacitar a desarrolladores en GitOps.
- Realizar pruebas de resiliencia y recuperación.

---

## 📌 Conclusión

Este laboratorio demuestra cómo el uso de ArgoCD y Helm permite transformar un flujo de despliegue tradicional en una experiencia automatizada, reproducible y trazable, optimizando los tiempos y reduciendo riesgos.

---