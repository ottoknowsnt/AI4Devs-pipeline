# Conversación con GPT-4o

## Usuario

Toma el rol de un senior Engineer Devops, primero de todo necesito que tomes el contexto del @Codebase , el objetivo aqui va a ser crear un pipeline en Github Actions que, tras el trigger "push a una rama con un Pull Request abierto", siga los siguientes pasos:

    Pase unos tests de backend.
    Genere un build del backend.
    Despliegue el backend en un EC2.

No hagas nada aun a nivel de codigo, dime como vas a llevar a cabo estos pasos y que dudas o preguntas tienes antes de comenzar

## GPT-4o

Para crear un pipeline en GitHub Actions que cumpla con los requisitos mencionados, seguiré los siguientes pasos:

1. **Entender el Contexto del Codebase**: Backend en TypeScript con Express, Prisma como ORM, pruebas en Jest, despliegue en EC2.
2. **Plan para el Pipeline**:
   - **Trigger**: Activar en `pull_request`.
   - **Ejecutar Pruebas**: `npm test`.
   - **Generar Build**: `npm run build`.
   - **Desplegar en EC2**: Usar `scp` y `pm2`.

### Preguntas:
- ¿Cómo están configuradas las pruebas?
- ¿El comando `npm run build` está listo?
- ¿Método actual para desplegar en EC2?
- ¿Variables de entorno en EC2?
- ¿Credenciales de AWS configuradas?

## Usuario

para las pruebas del backend, si te fijas en el @package.json , se usa jest para las pruebas unitarias
en el @package.json esta el comando: "start:prod": "npm run build && npm start" para hacer la build, haz los cambios que consideres necesario para este caso
para el despliegue del backend en EC2 se debe crear un nuevo workflow bajo @workflows usando Github Actions
Recomienda cual es la mejor forma para gestionar las variables de entorno del servidor EC2
Dime como debo configurar las credenciales de AWS y la direccion IP de la instancia EC2

## GPT-4o

Gracias por la información. Aquí está el plan detallado:

1. **Pipeline en GitHub Actions**:
   - **Trigger**: `pull_request`.
   - **Jobs**: Checkout, instalar dependencias, ejecutar pruebas, generar build, desplegar en EC2.

2. **Gestión de Variables de Entorno**: Usar un archivo `.env` en EC2.

3. **Credenciales de AWS**: Configurar en GitHub Secrets (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `EC2_INSTANCE_IP`).

### Ejemplo de Workflow:

```yaml
name: Deploy Backend to EC2
on:
  pull_request:
    branches:
      - main
``` 


## Usuario

cambia el nombre de @deploy-backend.yml por pipeline.yml

## GPT-4o

Para cambiar el nombre del archivo de workflow de `deploy-backend.yml` a `pipeline.yml`, simplemente actualiza el nombre del archivo en el directorio `.github/workflows`.

## Usuario

como tengo que configurar el EC2 para poder desplegar este repositorio ahi?

## GPT-4o

Para configurar tu instancia EC2:

1. **Acceso SSH**: Conéctate usando el archivo `.pem`.
2. **Instalar Node.js y npm**: Usa `curl` y `yum`.
3. **Instalar PM2**: `npm install -g pm2`.
4. **Configurar Nginx (opcional)**.
5. **Configurar Variables de Entorno**: Usa un archivo `.env`.
6. **Configurar SSH para Despliegue**: Asegúrate de que la clave pública esté en `~/.ssh/authorized_keys`.

## Usuario

se puede hacer esto a traves de la interfaz web? si es asi dame una guia de pasos

## GPT-4o

Sí, puedes configurar tu instancia EC2 a través de la interfaz web de AWS Management Console:

1. **Lanzar una Instancia EC2**: Usa Amazon Linux 2, configura el grupo de seguridad para permitir SSH.
2. **Conectar a la Instancia EC2**: Usa SSH.
3. **Configurar el Entorno**: Instala Node.js, npm, y PM2.
4. **Configurar Variables de Entorno**: Crea un archivo `.env`.
5. **Configurar Despliegue desde GitHub Actions**: Configura claves SSH y secretos en GitHub.

## Usuario

donde obtengo esas credenciales tras crear el usuario? no lo encuentro

## GPT-4o

Cuando creas un usuario en AWS IAM, las credenciales se muestran una sola vez. Si no las guardaste, puedes generar un nuevo par de claves:

1. **Accede a IAM**: Crea un nuevo usuario con acceso programático.
2. **Asignar Permisos**: Usa `AmazonEC2FullAccess` o una política personalizada.
3. **Obtener Credenciales**: Se muestran al crear el usuario. Si no las guardaste, genera nuevas en la pestaña "Security credentials".

## Usuario

ya he guardado las variables en el actions de Github, viendo el actual contenido de @pipeline.yml , el certificado pem donde deberia tenerlo ubicado? ya que en el @pipeline.yml se indica esto:

## GPT-4o

Para usar el archivo `.pem` en GitHub Actions:

1. **Guardar la Clave Privada en GitHub Secrets**: Copia el contenido del archivo `.pem` y guárdalo como `SSH_PRIVATE_KEY`.
2. **Modificar el Workflow**: Usa el secreto para crear un archivo temporal `private_key.pem` en el runner.

## Usuario

mi duda ahora esta aqui en el @pipeline.yml , cual deberia ser esa ruta?

:/path/to/deployment

## GPT-4o

La ruta `:/path/to/deployment` es el directorio en tu instancia EC2 donde deseas desplegar tu aplicación. Decide un directorio, por ejemplo, `/home/ec2-user/my-backend-app`, y asegúrate de que el usuario tenga permisos de escritura.

## Usuario

haz que el usuario y el directorio se guarden tambien en unas variables de entorno, actualiza el @pipeline.yml y dame los pasos necesarios para hacer esto

## GPT-4o

Para almacenar el usuario y el directorio de despliegue como variables de entorno:

1. **Configurar Secretos en GitHub**: Añade `EC2_USER` y `DEPLOYMENT_DIRECTORY` en GitHub Secrets.
2. **Actualizar el Archivo `pipeline.yml`**: Usa estos secretos en el script de despliegue.

## Usuario

dame los pasos para poder conectarme via ssh a la instancia EC2

## GPT-4o

Para conectarte a tu instancia EC2 a través de SSH:

1. **Archivo de Clave Privada (.pem)**: Asegúrate de tenerlo y que tenga permisos correctos (`chmod 400 your-key.pem`).
2. **Obtener la Dirección IP**: Desde la consola de AWS.
3. **Conectarse**: Usa `ssh -i your-key.pem ec2-user@your-ec2-public-ip`.