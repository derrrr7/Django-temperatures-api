# 🌡️ API RESTful para Gestión de Temperaturas de Ciudades

## Proyecto de Asignatura: Desarrollo de APIs Web

| Estudiante | Profesor | Fecha de la Implementación |
| :--- | :--- | :--- |
| **Derwin Viera** | **Elias Vargas** | Noviembre 2025 |

---

## 1. Implementación y Requisitos Cumplidos

Este proyecto implementa una **API RESTful** utilizando **Django** y **Django REST Framework (DRF)** para gestionar datos de temperaturas.

Se han cumplido todos los requisitos del enunciado:

* **Modelo `CityTemperature`**: Definido con los campos requeridos: `city` (CharField), `temperature` (DecimalField), y `last_updated` (DateTimeField auto-actualizable).
* **Endpoints CRUD**: Se utiliza el `ModelViewSet` para generar automáticamente los 6 endpoints (Listar, Crear, Leer Detalle, Actualizar Parcial/Total y Eliminar).
* **Serialización**: Implementado en `temperatures/serializers.py`.
* **Localización**: Configurado con `LANGUAGE_CODE = 'es'` y `TIME_ZONE = 'America/Caracas'` en `settings.py` (La interfaz de administrador y el título del API Root aparecen en español, demostrando la correcta configuración).
* **Autenticación y Permisos**: El requisito clave (lectura pública y escritura autenticada) se cumple mediante el uso de **Token Authentication**.

---

## 2. Instrucciones de Instalación (Paso a Paso)

Para poner en marcha la API, por favor siga estos pasos:

### 2.1. Preparación del Entorno

1.  **Descomprimir el Archivo:** Coloque la carpeta del proyecto (`weather_api/`) en la ubicación deseada.
2.  **Abrir la Terminal:** Navegue hasta la carpeta principal del proyecto.
3.  **Crear y Activar el Entorno Virtual:** (Recomendado para evitar conflictos)
    ```bash
    python -m venv venv
    # En Windows CMD/PowerShell:
    .\venv\Scripts\activate
    # En Linux/macOS:
    source venv/bin/activate
    ```

### 2.2. Instalación de Dependencias

Instale las librerías necesarias (Django, DRF, etc.) utilizando el archivo `requirements.txt`:

```bash
pip install -r requirements.txt
```
###2.3. Configuración Inicial de la Base de Datos
Ejecute las migraciones para crear las tablas necesarias, incluyendo el modelo CityTemperature y las tablas de autenticación:
```
python manage.py migrate
```
### 2.4. Ejecución del Servidor
El servidor estará activo y listo para recibir peticiones:
```
python manage.py runserver
```
### 3. Credenciales de Prueba y Seguridad
La API requiere un usuario autenticado para las operaciones de escritura (POST, PUT, DELETE). Para la revisión, se ha creado el siguiente superusuario de prueba:
```
Credencial	Usuario	Contraseña
Login de Prueba:derwinviera	Enrique1234
```
### 3.1. Prueba Clave: Verificación de la Seguridad (POST)
Utilice un cliente HTTP (como Postman o Insomnia) para confirmar que la protección funciona:
```
Paso 1: Obtener el Token (Login)
Se utiliza el endpoint de DRF para autenticarse y recibir el token que da acceso.

Método: POST

URL: http://127.0.0.1:8000/api-token-auth/

Body (x-www-form-urlencoded):

username: derwinviera

password: prueba1234

Resultado Esperado: Código 200 OK con el token (Ej: "token": "80900afd...")

Paso 2: Fallo Intencional (Prueba de Seguridad)
Intentar crear un registro sin enviar la cabecera de autenticación.

Método: POST

URL: http://127.0.0.1:8000/api/temperatures/

Headers: NO incluir la cabecera Authorization.

Resultado Esperado: Código 401 Unauthorized y mensaje "Las credenciales de autenticación no se proveyeron." (Seguridad Confirmada)

Paso 3: Éxito con Token (Crear Registro Protegido)
Utilizar el token obtenido en el Paso 1 para crear el registro.

Método: POST

URL: http://127.0.0.1:8000/api/temperatures/

Headers:

Content-Type: application/json

Authorization: Token [PEGA AQUÍ EL TOKEN DE LA CLAVE 3.1] (Debe haber un espacio entre la palabra Token y el token largo).

Body (raw, JSON):

JSON

{
    "city": "Maracaibo",
    "temperature": 35.20
}
Resultado Esperado: Código 201 Created con el objeto JSON del nuevo registro.
```
### 4. Endpoints Generados por ModelViewSet
Todos los endpoints cumplen con los métodos HTTP estándar:
```
Método	URL	Propósito	Permisos
GET	/api/temperatures/	Listar todas las temperaturas.	Público
POST	/api/temperatures/	Crear un nuevo registro.	Autenticado
GET	/api/temperatures/{pk}/	Leer los detalles de una temperatura específica.	Público
PUT	/api/temperatures/{pk}/	Actualizar el registro completo.	Autenticado
DELETE	/api/temperatures/{pk}/	Eliminar un registro.	Autenticado

