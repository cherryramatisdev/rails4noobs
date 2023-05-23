# Linguagem

## Instalando ruby

<p align="center">
    <img src="./imgs/2023-05-23-00-11-06.png" width="120" />
</p>

Está parte pode ser encontrada no [ruby4noobs](https://github.com/Rinyaresu/ruby4noobs/blob/master/src/2-Ambiente/2-configuracao-de-ambiente.md)
<p align="center">
    <img src="./imgs/2023-05-23-09-57-35.png" width="250" />
</p>

## Instalando sqlite

Antes de instalarmos o ruby on rails de fato, precisamos instalar um banco de dados para que possamos desenvolver nossa aplicação com uma camada de persistência(visto que o rails já vem configurado por padrão).
Para esse tutorial vamos utilizar o `sqlite3` por ser um banco de dados simples.

### MacOS

Para o MacOS, simplesmente utilize o [homebrew](https://brew.sh) para instalar

```bash
brew install sqlite3
```

### Windows

Para instalar no windows pode-se seguir a documentação no site oficial do [sqlite download](https://www.sqlite.org/download.html)

### Linux (Debian/Ubuntu)

Para linux ou WSL2 pode-se simplesmente instalar via `apt`

```bash
sudo apt install sqlite3
```

<p align="center">
    <img src="./imgs/2023-05-23-09-59-15.png" width="250" />
</p>

## Instalando ruby on rails

Para instalar ruby on rails vamos utilizar um comando que veio junto a instalação do ruby chamado `gem`, para isso execute o seguinte comando no seu terminal:

```sh
gem install rails bundler
```

> Bundler é util para lidar com o arquivo Gemfile no nosso projeto.

Próximo: [Entendendo MVC](Arquitetura/MVC.md)
