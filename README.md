# Apresentação do projeto Download Box

Sonarr / Radarr / Prowlarr / Bazarr / Transmission / Jellyfin

Baixe programas de TV e filmes, classifique, com a qualidade e legendas desejadas, pronta para assistir, em um belo media player. Tudo automatizado.

## Hardware utilizado

TV Box HK1 X3 com a seguinte configuração:

- CPU: Amlogic S905X3 64-bit quad-core ARM® Cortex™ A55 CPU
- GPU: G31 MP2 GPU processor
- RAM: DDR3 4GB
- ROM: eMMC 128GB
- Rede: GigabitEthernet RJ-45 / WiFi: 802.11 a/b/g/n 2.4G / 5G
- SO: Armbian 22.05.0-trunk Focal (baseado no Ubuntu 20.04.4 LTS)
- Docker versão 20.10.14, build a224086
- docker-compose versão 1.25.0
- Portainer 2.22.1

Foi utilizado o modelo mencionado por ter rede padrão GigabitEthernet, mas pode ser qualquer outro que tenha CPU S905X e 2GB de RAM no mínimo.

## Pré requisitos

- Armbian (disponível em https://github.com/ophub/amlogic-s9xxx-armbian/releases). Não será abordado a instalação/configuração (está disponível em https://github.com/ophub/amlogic-s9xxx-armbian/blob/main/README.md)
- Pacotes ```git docker docker-compose```

## Visão geral do projeto

Configuração realizada em casa para lidar com download, classificação e reprodução automatizada de séries de TV e filmes.

_**Isenção de responsabilidade: não estou incentivando/apoiando a pirataria, isso é apenas para fins informativos.**_

Como funciona? Confio em várias ferramentas integradas. Elas são todas de código aberto e implantadas como contêineres do Docker.

O fluxo de trabalho comum será detalhado a seguir para dar uma ideia de como as coisas funcionam.

## Sonarr e Radarr: monitoramento de séries de TV e filmes

Usando a interface web **[Sonarr](https://sonarr.tv/)**, é possível buscar um programa de TV pelo nome e marcá-lo como monitorado. Também é possível especificar um idioma e a qualidade necessária (1080p, por exemplo). O Sonarr cuidará automaticamente da análise de episódios e temporadas existentes deste programa de TV. Ele compara o que você tem no disco com o cronograma de lançamento do programa de TV e aciona o download dos episódios ausentes. Ele também se encarrega de atualizar seus episódios existentes se houver uma qualidade melhor que corresponda aos seus critérios.

Sonarr processa lotes de download para temporadas inteiras. Mas também lida com os próximos episódios e temporadas em tempo real. Nenhuma intervenção humana é necessária durante todo o processo. Quando o download termina, o Sonarr move o arquivo para o local apropriado e renomeia o arquivo, se necessário.

**[Radarr](https://radarr.video/)** é exatamente a mesma coisa, porém para filmes.

## Transmission: cliente torrent simples e leve

O Sonarr e o Radarr podem contar com duas maneiras diferentes de baixar arquivos: através de arquivos bin Usenet (grupos de notícias) ou através de torrents. Será configurado somente a opção Torrent utilizando o cliente **[Transmission Web](https://transmissionbt.com/)**.

## Prowlarr: indexadores de torrents com 

Os arquivos torrents são pesquisados automaticamente pelo Sonarr/Radarr através de uma lista de indexadores que você deve configurar. Indexadores são APIs que permitem a busca de lançamentos específicos organizados por categorias. Pense em navegar no Pirate Bay programaticamente. É por isso que usaremos outra ferramenta chamada **[Prowlarr](https://github.com/Prowlarr/Prowlarr/)**. É considerado como uma API de proxy local para os indexadores de torrent mais populares. Ele pesquisa e analisa informações de sites heterogêneos.

## Bazarr: legendas automáticas 

O **[Bazarr](https://www.bazarr.media/)** é usado para adicionar legendas nos episódios e filmes baixados, sem a necessidade de localizar e adicionar legendas de forma manual. Toda vez que um novo filme ou série é adicionada no Radarr ou no Sonarr, o Bazarr vai completar sua experiência adicionando a legenda no idioma escolhido.

## Jellyfin: software livre como ótima alternativa ao Plex e Emby

**[Jellyfin](https://jellyfin.org/)** é um sistema de mídia de software livre que permite que você controle o gerenciamento e o streaming de sua mídia através de um interface web amigável e simples, conectado a um servido. É uma alternativa ao Emby e Plex proprietários, para fornecer mídia de um servidor dedicado para dispositivos de usuário final por meio de vários aplicativos. Há aplicativos para plataformas mobile, SmartTV e Desktop.

## Heimdall: organizando tudo em uma dashboard

**[Heimdall](https://heimdall.site/)** é uma dashboard para todos os aplicativos do projeto. No entanto, pode adicionar links para o que quiser.

## Portainer: administração dos containers

**[Portainer](https://www.portainer.io/)** é uma interface web que interage com o socket do docker para criar novos contêineres e monitorá-los. Também pode ser utilizado para visualizar o cluster, gerenciar a autenticação de usuários e permissões de acesso ao cluster.

# Como instalar o ambiente:

```sh
mkdir /storage
git clone https://github.com/marcelobaptista/download-box.git /storage
cd /storage
docker-compose -f docker-compose.yml up -d
```
Ao término teremos a seguinte estrutura no ponto de pontagem /storage:
```bash
/storage
├── config
├── downloads
└── media
    ├── Filmes
    └── TV
```
# Como configurar o ambiente:

(Em breve detalharei)
