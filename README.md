# Comandos utilizados

### Mount Secret

```bash
docker buildx build --secret id=github_token,src=./my-github-token.txt -t test .
```

- **`--secret id=github_token,src=./my-github-token.txt`**: Disponibiliza um segredo durante o build, lendo seu valor do arquivo indicado, sem incorporá-lo às camadas da imagem.
- **`-t test`**: Define `test` como nome (tag) da imagem gerada.
- **`.`**: Define o diretório atual como contexto de build.

### Mount SSH

```bash
docker buildx build --ssh default -t test .
```

- **`--ssh default`**: Disponibiliza o agente SSH padrão durante o build, permitindo autenticação em serviços remotos, como o GitHub, sem copiar chaves privadas para a imagem.
- **`-t test`**: Define `test` como nome (tag) da imagem gerada.
- **`.`**: Define o diretório atual como contexto de build.


### Mount Bind e Mount Cache


```bash
docker buildx build -t test --progress=plain .
```

- **`-t test`**: Define `test` como nome (tag) da imagem gerada.
- **`--progress=plain`**: Exibe o progresso do build em formato de texto simples, mostrando detalhadamente as etapas e suas respectivas saídas.
- **`.`**: Define o diretório atual como contexto de build.

### Cache Storage Backends

```bash
docker buildx build -t test --cache-from=type=local,src=./buildx-cache --cache-to=type=local,dest=./buildx-cache .
```

- **`-t test`**: Define `test` como nome (tag) da imagem gerada.
- **`--cache-from=type=local,src=./buildx-cache`**: Utiliza o cache de build armazenado no diretório `./buildx-cache` para acelerar a construção da imagem.
- **`--cache-to=type=local,dest=./buildx-cache`**: Exporta o cache gerado durante o build para o diretório `./buildx-cache`, permitindo reutilizá-lo em builds futuros.
- **`.`**: Define o diretório atual como contexto de build.

```bash
docker buildx build -t devpontes/test:latest --cache-from=type=local,src=./buildx-cache --cache-to=type=registry,ref=devpontes/test:buildcache .
```

- **`-t devpontes/test:latest`**: Define o nome e a tag (`latest`) da imagem gerada.
- **`--cache-from=type=local,src=./buildx-cache`**: Utiliza o cache de build armazenado localmente no diretório `./buildx-cache` para acelerar a construção da imagem.
- **`--cache-to=type=registry,ref=devpontes/test:buildcache`**: Exporta o cache de build para um registry Docker, utilizando `devpontes/test:buildcache` como referência, permitindo compartilhá-lo e reutilizá-lo em outros ambientes.
- **`.`**: Define o diretório atual como contexto de build.


```bash
docker buildx build -t devpontes/test:latest --cache-to=type=inline -f Dockerfile.base .
```

- **`-t devpontes/test:latest`**: Define o nome e a tag (`latest`) da imagem gerada.
- **`--cache-to=type=inline`**: Incorpora os metadados do cache de build à imagem gerada, permitindo reutilizá-los em builds futuros.
- **`-f Dockerfile.base`**: Especifica o arquivo `Dockerfile.base` como referência para a construção da imagem.
- **`.`**: Define o diretório atual como contexto de build.

```bash
docker buildx build -t devpontes/test:base --cache-from=type=registry,ref=devpontes/test:base --cache-to=type=inline -f Dockerfile.base .
```

- **`-t devpontes/test:base`**: Define o nome e a tag (`base`) da imagem gerada.
- **`--cache-from=type=registry,ref=devpontes/test:base`**: Utiliza o cache de build armazenado no registry Docker, referenciado por `devpontes/test:base`, para acelerar a construção da imagem.
- **`--cache-to=type=inline`**: Incorpora os metadados do cache de build à imagem gerada, permitindo reutilizá-los em builds futuros.
- **`-f Dockerfile.base`**: Especifica o arquivo `Dockerfile.base` como referência para a construção da imagem.
- **`.`**: Define o diretório atual como contexto de build.

### Execução


```bash
docker run --rm test
```

- **`--rm`**: Remove automaticamente o container após sua execução.
- **`test`**: Define a imagem utilizada para criar e executar o container.


```bash
docker compose build
```

- **`docker compose build`**: Constrói ou reconstrói as imagens dos serviços definidos no arquivo Docker Compose, sem iniciar os containers.

```bash
docker compose run app
```

- **`docker compose run app`**: Cria e executa um novo container a partir do serviço `app` definido no Docker Compose, sem iniciar os demais serviços automaticamente.
