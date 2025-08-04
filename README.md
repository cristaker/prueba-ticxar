#  Servicio de Autenticación con Registro de Login

**Autor:** Christian Sánchez

## Instrucciones de ejecución

1. URL del repositorio:
   ```
   https://github.com/cristaker/prueba-ticxar

2. Asegúrate de tener Java 21+ y Maven instalados.

3. Ejecuta el proyecto
   ```
   ./mvnw spring-boot:run
4. El servicio estará disponible en http://localhost:8080

5. Usuario y contraseña de prueba
   ```
   Usuario: emilys
   Contraseña: emilyspass

6. Ejemplo de curl válido:
   ```
   curl --request POST \
   --url https://dummyjson.com/auth/login \
   --header 'Content-Type: application/json' \
   --data '{
   "username": "emilys",
   "password": "emilyspass"
   }'
7. Respuesta esperada
    ```
   {
    "id": 1,
    "username": "emilys",
    "email": "emily.johnson@x.dummyjson.com",
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwidXNlcm5hbWUiOiJlbWlseXMiLCJlbWFpbCI6ImVtaWx5LmpvaG5zb25AeC5kdW1teWpzb24uY29tIiwiZmlyc3ROYW1lIjoiRW1pbHkiLCJsYXN0TmFtZSI6IkpvaG5zb24iLCJnZW5kZXIiOiJmZW1hbGUiLCJpbWFnZSI6Imh0dHBzOi8vZHVtbXlqc29uLmNvbS9pY29uL2VtaWx5cy8xMjgiLCJpYXQiOjE3NTQyNjQ0NjcsImV4cCI6MTc1NDI2ODA2N30.NdTmiE3q5tQ6vDaQHxcGU8Ay-_52R_CLiaD4iDTi4ec",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwidXNlcm5hbWUiOiJlbWlseXMiLCJlbWFpbCI6ImVtaWx5LmpvaG5zb25AeC5kdW1teWpzb24uY29tIiwiZmlyc3ROYW1lIjoiRW1pbHkiLCJsYXN0TmFtZSI6IkpvaG5zb24iLCJnZW5kZXIiOiJmZW1hbGUiLCJpbWFnZSI6Imh0dHBzOi8vZHVtbXlqc29uLmNvbS9pY29uL2VtaWx5cy8xMjgiLCJpYXQiOjE3NTQyNjQ0NjcsImV4cCI6MTc1Njg1NjQ2N30.cPGZnxuoP2IDjRasrPxVeU4gBdMM8MaOhHnvZFQ7pHo"
   }

## Guardado

Cada vez que un usuario inicia sesión exitosamente:

1. Se realiza una llamada al servicio externo con los datos del usuario.
2. Si la autenticación es exitosa, se recibe una respuesta (LoginResponseDto).
3. Esta respuesta se convierte a una entidad LoginLog mediante el mapper LoginLogMapper.
4. Finalmente, la información se guarda en la base de datos con el repositorio LoginLogRepository.

Datos registrados:
 ```
 id
 username
 loginTime (fecha y hora del inicio de sesión)
 accessToken
 refreshToken
 ```
Esto permite llevar un control detallado de los inicios de sesión de los usuarios.

## Postman
En la raíz del proyecto se agregó la colección de Postman que incluye:

1. Endpoint de login para el registro.

2. Endpoint de consulta de datos relevantes.

