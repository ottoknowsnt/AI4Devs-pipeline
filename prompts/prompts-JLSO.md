# prompts - pipeline-JLSO

| Author         | Jorge Luis Sánchez Ocampo |
| -------------- | ------------------------- |
| Code Assistant | Cursor IDE                |
| LLM            | Claude-3.5-sonnet         |

```markdown
@Codebase Crea el archivo de configuración para ci/cd con el workflow de github actions para el @backend que cumpla con lo siguiente: 1. Pasar todos los tests del backend 2. Generar un build del backend 3. Despliegar el backend en un EC2 4. Asegúrate de que el pipeline se dispare con un push a la rama main cuando esta tenga un Pull Request abierto
```

```markdown
now change the github actions branch config from main to pipeline-JLSO
```

```markdown
what could be the next steps to test the ci/cd workflow?
```

```markdown
@backend how to ensure that the ec2 instance has all the necesary to run the backend project?
```

```markdown
do i have to accept the pull request to trigger de deploy job? or when is supose to be executed?
```

```markdown
i have this error in the "deploy to EC2" step: Run echo "$PRIVATE_KEY" > private_key.pem
  echo "$PRIVATE_KEY" > private_key.pem
chmod 600 private_key.pem

# Crear directorio de la aplicación si no existe

ssh -o StrictHostKeyChecking=no -i private_key.pem ${USER}@${HOST} '
mkdir -p ~/app/backend
'

# Copiar archivos al servidor

scp -o StrictHostKeyChecking=no -i private_key.pem -r backend/\* ${USER}@${HOST}:~/app/backend/

# Instalar dependencias y reiniciar la aplicación

ssh -o StrictHostKeyChecking=no -i private_key.pem ${USER}@${HOST} '
cd ~/app/backend
npm ci --production
npx prisma generate
pm2 delete backend || true
pm2 start dist/index.js --name backend
'

rm -f private\*key.pem
shell: /usr/bin/bash -e {0}
env:
AWS*DEFAULT_REGION: eu-west-1
AWS_REGION: eu-west-1
AWS_ACCESS_KEY_ID: \*\**
AWS*SECRET_ACCESS_KEY: **\*
PRIVATE_KEY: ***
HOST: \_\*\*
USER: ec2-user

Warning: Permanently added '**_' (ED25519) to the list of known hosts.
ec2-user@_**: Permission denied (publickey).
Error: Process completed with exit code 255.
```

```markdown
the region configured in aws ec2 instance is: us-east-1
```

```markdown
@backend Error: RROR] Process or Namespace backend not found. is this an critical error?, the backend is already deployed in the ec2 instance
```
