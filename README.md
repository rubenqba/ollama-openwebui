# OpenWebUI con Docker Compose

Este repositorio contiene docker compose file para la aplicación OpenWebUI. OpenWebUI es una aplicación para utilizar los modelos de Ollama y OpenAI que se desplegar en un servidor.

## Descripción de servicios

El servicio `openwebui` se basa en la imagen `ghcr.io/open-webui/open-webui:ollama` por lo que ya incluye el servicio de [Ollama](https://ollama.com). Este servicio es un miembro de una red llamada por defecto _proxy_, en caso que se necesite agregarla a otra diferente solo defina el valor de la variable de ambiente `PROXY_NETWORK_NAME`. Se espera que esta red se haya creado antes de ejecutar `docker-compose up`.

También se requiere de un volumen `openwebui` que se utiliza para almacenar los datos de la base de OpenWebUI. Este volumen se maneja como externo para cubir cualquier requerimiento especifico que necesite definir. Si por el contrario desea utilizar otro volumen solo sobreescriba la variable de ambiente `OPENWEBUI_VOLUME_NAME`. De igual forma para persistir los datos de los modelos descargados por Ollama se utiliza el volumen `OLLAMA_VOLUME_NAME`, por defecto se denomina `ollama`.

Además, debe configurar una clave maestra de `WEBUI_SECRET_KEY`. Esto debe ser una cadena aleatoria segura. No se debe perder esta clave, ya que se utiliza para firmar los tokens de autenticación.

## Despliegue de la aplicación

Antes de iniciar la aplicación, debes asegurarte tener [Docker](https://docs.docker.com/engine/install/) y [Docker Compose](https://docs.docker.com/compose/install/) instalados.

Los pasos para crear la red y el volumen no serán explicados aquí. Usted puede utilizar las configuraciones que desee siguiendo la metodología que estime combeniente para sus requerimientos.

Luego, para lanzar la aplicación, primero debes configurar todas las variables de entorno necesarias. Puedes hacerlo en la línea de comandos o configurarlas en un archivo `.env`.

Una vez que las variables de entorno estén configuradas, puedes desplegar la aplicación con el siguiente comando:

```bash
docker compose up -d
```

Ahora tu aplicación OpenWebUI debería estar desplegada y lista para ser utilizada. El puerto por defecto de la aplicación es `8080`.

## Comandos de Docker útiles

- `docker-compose up -d` para iniciar la aplicación.
- `docker-compose down` para detener la aplicación.
- `docker-compose logs` para ver los registros de la aplicación.
- `docker-compose ps` para ver el estado de los servicios de la aplicación.
