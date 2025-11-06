# 🌡️ API RESTful para Gestión de Temperaturas de Ciudades

## Proyecto de Asignatura: Desarrollo de APIs Web

| Estudiante | Profesor | Fecha de Entrega |
| :--- | :--- | :--- |
| **Derwin Viera** | Elias Vargas | Noviembre 2025 |

---

## 1. Introducción y Requisitos del Proyecto

Este proyecto implementa una **API RESTful** utilizando **Django** y **Django REST Framework (DRF)** para gestionar registros de temperatura de diferentes ciudades.

Se han cumplido todos los requisitos solicitados, incluyendo:

1.  **Modelo `CityTemperature`**: Contiene campos para `city` (CharField), `temperature` (DecimalField), y `last_updated` (DateTimeField auto-actualizable).
2.  **Endpoints CRUD**: Implementación automática de todos los métodos CRUD (`GET`, `POST`, `PUT`, `DELETE`) gracias al uso de `ModelViewSet`.
3.  **Serialización**: Uso de `ModelSerializer` para el modelo `CityTemperature`.
4.  **Autenticación de Lectura/Escritura**: El acceso de lectura (`GET`) es público, mientras que la escritura (`POST`, `PUT`, `DELETE`) requiere un token de autenticación.

---

## 2. Puesta en Marcha (Instalación y Ejecución)

A continuación, se detallan los pasos para instalar y ejecutar el proyecto desde la terminal:

### Requisitos Previos

* **Python 3.x**
* **pip** (Administrador de paquetes de Python)

### 2.1. Instalación de Dependencias

1.  Abrir la terminal y navegar hasta la carpeta raíz del proyecto (`weather_api/`).
2.  Crear y activar un entorno virtual (recomendado):
    ```bash
    python -m venv venv
    # En Windows:
    .\venv\Scripts\activate
    # En Linux/macOS:
    source venv/bin/activate
    ```
3.  Instalar todas las librerías necesarias (Django, DRF, djangorestframework-authtoken):
    ```bash
    pip install -r requirements.txt
    ```

### 2.2. Configuración de la Base de Datos

Ejecutar las migraciones para crear las tablas, incluyendo el modelo `CityTemperature` y las tablas de autenticación:

```bash
python manage.py migrate
