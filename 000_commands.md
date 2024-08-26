# Comandos básicos do Docker

## **Estrutura básica**

## docker \<objeto> \<comando> \<opções>

**Objetos mais usados**

- image
- container
- volume
- network
- system

### 1.1 docker image pull \<imagem>
Baixa uma imagem em um repósitorio de imagens do Docker

![alt text](001_docker_image_pull.png)

## OBS:
    - Imagem: nginx
    - Tag: alpine3.19

### 1.2 docker image ls
Lista as imagens contidas no Docker

![alt text](002_docker_image_ls.png)

### 1.3 docker image ls -q
Lista apenas o ID das imagens contidas no Docker

![alt text](003_docker_image_ls_-q.png)

### 1.4 docker image inspect
Traz informações específicas sobre uma imagem

```
docker image inspect nginx:alpine3.19
```

![alt text](004_docker_image_inspect.png)

### 1.5 docker image save
Salva uma imagem em um arquivo compactado

OBS: importante realizar o comando no terminal com o local de destino previamente definido:

```
cd OneDrive/Documentos/Studies/Docker
```

```
docker image save nginx.alpine3.19 -o alpine.tar
```

* **-o**: output (nome que será dado ao arquivo compactado que armazenará a imagem)

![alt text](005_docker_image_save.png)

### 1.6 docker image rm
Remove uma imagem do host

Pode se usar o nome da imagem e sua tag:
```
docker image rm nginx:alpine3.19
```

Ou o ID da imagem:
```
docker image rm 1ae23480369f
```

### 1.7 docker image load
Descompacta uma imagem compactada em arquivo e carrega no host

```
docker image load -i alpine.tar
```

* **-i**: input (nome do arquivo a ser descompactado)

![alt text](006_docker_image_load.png)

### 2.1 docker container run
Cria um container baseado em uma imagem do host

```
docker container run nginx:3.19
```

#### Parâmetros importantes

- -d (dettached mode): vai rodar o container sem prender o usuário no terminal
- -i (interactive mode): modo interativo
- -t (terminal): cria um terminal organizado
- --name (nome): concede um nome ao container

```
docker container run -it --entrypoint /bin/sh nginx:3.19
```

![alt text](007_docker_container_run_-it_--entrypoint.png)

```
docker container run -d --name "alpine" nginx:alpine:3.19
```

![alt text](008_docker_container_run_-d_--name_alpine.png)

### 2.2 docker container create
Cria um container sem executá-lo automaticamente

```
docker container create --name nginx-2 nginx:alpine3.19
```

![alt text](009_docker_container_create.png)

### 2.3 docker container start
Inicializa o container criado

```
docker container start <nome-do-container> OU <id-do-container>
```

![alt text](010_docker_container_start.png)

### 2.4 docker container stop
Parada sutil, graciosa, do container. Verifica se há algum processo rodando e aguarda a sua finalização

```
docker container stop <nome-do-container> OU <id-do-container>
```

![alt text](011_docker_container_stop.png)

### 2.5 docker container kill
Parada imediata do container

```
docker container kill <nome-do-container> OU <id-do-container>
```

![alt text](012_docker_container_kill.png)

### 2.6 docker container pause
Congela o container, mas não o paraliza totalmente

```
docker container pause <nome-do-container>
```

![alt text](013_docker_container_pause.png)

### 2.7 docker container unpause
Descongela o container

```
docker container unpause <nome-do-container>
```

![alt text](014_docker_container_unpause.png)

### 2.8 docker container rm
Remove o container do host

```
docker container rm <nome-do-container>
```

**OBS**: Para remover um container que está em execução:
```
docker container rm <nome-do-container> --force
```

![alt text](015_docker_container_rm.png)

### 2.9 docker container restart
Reinicia o container (bom para executar atualizações ou dar reboot no container)

```
docker container restart
```

![alt text](016_docker_container_restart.png)

### 2.10 docker container rename
Renomeia um container existente

```
docker container rename <nome-atual-do-container> <nome-novo-do-container>
```

![alt text](017_docker_container_rename.png)

### Associando porta do host à uma porta do container

```
docker container run -dt --name nginx -p 8080:80 nginx:1.23.1
```

* -d: dettached mode
* -t: cria um terminal
* -p: estabelece a porta do host (8080) e a porta selecionada de entrada do container (80)

![alt text](018_docker_container_run_-p.png)

![alt text](019_docker_container_run_-p_welcome-to-nginx.png)

```
docker container run -dt --name mysql --entrypoint /bin/sh -P mysql:8.0.30
```

* --entrypoint: __a preencher__
* -P: estabelece portas aleatórias no lado do host

![alt text](020_docker_container_run_-P.png)

### 2.11 docker container inspect
Retorna um JSON com todas as informações relacionadas ao container

![alt text](021_docker_container_inspect.png)

### 2.12 docker container port
Retorna todas as portas associadas ao container

![alt text](022_docker_container_port.png)

### 2.13 docker container diff
Indica todas as alterações executadas desde a primeira execução do container

- Criei o arquivo arquivo-teste.txt no container
![alt text](023_docker_container_diff_1.png)

- Vou verificar as diferenças em um outro terminal com o comando diff
![alt text](024_docker_container_diff_2.png)

### 2.14 docker container logs
Retorna os logs do container

* -f: prende o terminal e retorna em tempo real todos os processos realizados no container