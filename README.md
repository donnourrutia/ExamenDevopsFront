# 🖥️ Innovatech Chile - Aplicación Web

Proyecto correspondiente a la interfaz web utilizada para operar la plataforma logística de Innovatech Chile. Desde esta aplicación es posible consultar pedidos, visualizar información de despachos y gestionar distintas operaciones relacionadas con la distribución de productos.

## ✨ Funcionalidades Principales

* Consulta de órdenes registradas.
* Visualización del estado de despachos.
* Gestión de procesos logísticos.
* Comunicación con los servicios backend mediante API REST.
* Escalamiento automático de réplicas mediante Kubernetes Horizontal Pod Autoscaler (HPA).

## 🧰 Tecnologías Utilizadas

* React
* Vite
* Node.js
* Docker
* Kubernetes
* Amazon EKS
* Amazon ECR
* Horizontal Pod Autoscaler (HPA)

## 🚀 Configuración del Entorno

### Dependencias necesarias

* Node.js 16+
* npm o yarn

### Descarga del proyecto

```bash
git clone https://github.com/DoomedPlayer/DevopsEV3-front.git
```

### Instalación de paquetes

```bash
npm install
```

### Variables de entorno

Crear un archivo `.env` en la raíz del proyecto:

```env
VITE_URL_VENTAS=http://localhost:8082
VITE_URL_DESPACHOS=http://localhost:8081
```

Las direcciones pueden modificarse dependiendo del entorno donde se despliegue la aplicación.

### Inicio del servidor local

```bash
npm run dev
```

## 🌍 Despliegue en la Nube

La aplicación se empaqueta como una imagen Docker y se despliega en un clúster de **Amazon EKS**.

El acceso de los usuarios se realiza mediante un **LoadBalancer** de Kubernetes, encargado de distribuir el tráfico entre las distintas réplicas disponibles del frontend.

El almacenamiento de imágenes Docker se realiza en **Amazon ECR**, desde donde Kubernetes obtiene la versión más reciente para su despliegue.

## 📈 Escalamiento Automático

La aplicación utiliza **Horizontal Pod Autoscaler (HPA)** para adaptar automáticamente la cantidad de réplicas del Deployment según la carga del sistema.

El HPA monitorea el consumo de recursos del clúster y, cuando la utilización de CPU supera el umbral configurado, incrementa el número de Pods disponibles. Cuando la demanda disminuye, reduce las réplicas de manera automática para optimizar el uso de recursos.

Esta estrategia permite:

- Mejorar la disponibilidad del servicio.
- Distribuir la carga entre múltiples Pods.
- Optimizar el consumo de recursos del clúster.
- Mantener un rendimiento estable durante períodos de alta demanda.

## 🔄 Flujo de Entrega Continua

Cada actualización enviada a la rama principal activa automáticamente un pipeline de GitHub Actions.

### Etapas del pipeline

1. Instalación de dependencias del proyecto.
2. Compilación de la aplicación React.
3. Creación de la imagen Docker.
4. Publicación de la imagen en Amazon ECR.
5. Actualización automática del Deployment en Kubernetes.
6. Mantenimiento del escalamiento automático mediante Horizontal Pod Autoscaler.

La configuración sensible utilizada durante el proceso se administra mediante GitHub Secrets, manteniendo protegidas las credenciales de acceso a los servicios de AWS.

