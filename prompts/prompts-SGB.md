# IDE utilizado

Cursor con Claude 3.7 Sonnet Thinking (Agent)

# Prompts utilizados

## Checkout del repositorio

```
El proyecto ya está listo para pasar a producción, por lo que ahora necesitamos los pipelines adecuados de CI/CD que nos permitan hacerlo en condiciones.

Para empezar, se requiere el siguiente pipeline:

- Workflow de Github Actions, implementado en el archivo `github/workflows/deploy.yml`.
- Ejecutado cuando se realiza un push a una rama con un Pull Request abierto.
- De momento solo contendrá la configuración necesaria para hacer checkout del repositorio.
```

## Ejecución de tests de backend

```
¡Perfecto! Continuemos añadiendo más pasos a nuestro workflow:

- Añadir un paso adicional para ejecutar los tests de backend.
- En el archivo `README.md` se detalla como configurar correctamente el backend.
- En el archivo `backend/package.json` se incluye un script para correr todos los tests de backend.
```

## Generación de build del backend

```
¡Genial! Ahora necesitaremos añadir otro paso adicional al workflow:

- Añadir un paso más para generar una build del backend.
- En el archivo `README.md` se detalla como realizarlo.
```

## Despliegue del backend en EC2

```
¡Increíble! Ya solo necesitamos el paso final de nuestro workflow:

- Añadir un paso que despliegue el backend en un EC2.
- En el archivo `README.md` se detalla la configuración necesaria para poder desplegar el backend a un EC2, comprueba así que nuestro proyecto esté configurado correctamente, y realiza las configuraciones necesarias si no es así.
- La instancia EC2 ya está creada y configurada, y las variables necesarias ya están configuradas como secretos del repositorio.
```

Fueron necesarios los siguientes prompts para mejorar el workflow generado:

```
Un par de mejoras:

1. Puedes usar la acción `easingthemes/ssh-deploy`para simplificar el deploy.
2. Los únicos secretos disponibles son los definidos en el `README.md`. Estos son: `AWS_ACCESS_ID`, `AWS_ACCESS_KEY` y `EC2_INSTANCE`.
```

```
Te comento las últimas mejoras:

1. El secreto `AWS_ACCESS_ID` contiene el nombre de usuario remoto.
2. La acción `easingthemes/ssh-deploy` permite ejecutar comandos después de la sincronización con la variable `SCRIPT_AFTER`, no es necesaria la acción `appleboy/ssh-action`.
```
