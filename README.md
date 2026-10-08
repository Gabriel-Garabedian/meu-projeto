# Site estático em container Docker (Debian + nginx)

**Aluno:** Gabriel da Silva Der Garabedian
**Disciplina:** SUA DISCIPLINA
**Data:** 08/10/2026

## Descrição
Site estático servido por nginx dentro de um container Docker criado a partir da imagem `debian:trixie`. Os arquivos do site ficam no `meu_site.tar`, extraído para `/var/www/html/` via `ADD` no Dockerfile.

## Estrutura
```
meu_projeto/
├── Dockerfile
├── meu_site.tar
├── site/              # arquivos-fonte (index.html)
├── evidencias/        # logs e prints
├── executar.ps1       # build + run + geração de evidências
└── README.md
```

## Como executar
```powershell
docker build -t meu_site .
docker run -d --name meu_site -p 8090:80 meu_site
```
Acesse: http://localhost:8090

## Como verificar
```powershell
docker ps
curl.exe -i http://localhost:8090
docker logs meu_site
```
Resposta esperada: `HTTP/1.1 200 OK` e a página "Meu site rodando em container Docker".

## Como atualizar o site
```powershell
tar -cf meu_site.tar -C site .
docker rm -f meu_site
docker build -t meu_site .
docker run -d --name meu_site -p 8090:80 meu_site
```

## Parar e remover
```powershell
docker stop meu_site
docker rm meu_site
```

## Evidências
- Saídas de comandos: [evidencias/evidencias.txt](evidencias/evidencias.txt)
- Build concluído: ![build](evidencias/build.png)
- Container em execução: ![docker ps](evidencias/docker-ps.png)
- Site no navegador: ![navegador](evidencias/navegador.png)

