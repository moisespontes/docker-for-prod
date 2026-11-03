# Comandos utilizados

### Mount Secret

```bash
docker buildx build --secret id=github_token,src=./my-github-token.txt -t test .
```

- **`--secret id=github_token,src=./my-github-token.txt`**: Disponibiliza um segredo durante o build, lendo seu valor do arquivo indicado, sem incorporá-lo às camadas da imagem.
- **`-t test`**: Define `test` como nome (tag) da imagem gerada.
- **`.`**: Define o diretório atual como contexto de build.



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
