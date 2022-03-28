# Download Box

Sonarr / Radarr / Prowlarr / Bazarr / Transmission / Jellyfin

Baixe programas de TV e filmes, classifique, com a qualidade e legendas desejadas, pronta para assistir, em um belo media player. Tudo automatizado.

## Visão geral

Isso é o que eu configurei em casa para lidar com download, classificação e reprodução automatizados de programas de TV e filmes.

_Isenção de responsabilidade: não estou incentivando/apoiando a pirataria, isso é apenas para fins informativos._

Como funciona? Confio em várias ferramentas integradas. Eles são todos de código aberto e implantados como contêineres do Docker no meu servidor Linux.

O fluxo de trabalho comum é detalhado nesta primeira seção para dar uma ideia de como as coisas funcionam.

## Monitoramento de séries de TV e filmes com Sonarr e Radarr

Usando a interface web **[Sonarr](https://sonarr.tv/)**, é possível buscar um programa de TV pelo nome e marcá-lo como monitorado. Também é possível especificar um idioma e a qualidade necessária (1080p, por exemplo). O Sonarr cuidará automaticamente da análise de episódios e temporadas existentes deste programa de TV. Ele compara o que você tem no disco com o cronograma de lançamento do programa de TV e aciona o download dos episódios ausentes. Ele também se encarrega de atualizar seus episódios existentes se houver uma qualidade melhor que corresponda aos seus critérios.

Sonarr processa lotes de download para temporadas inteiras. Mas também lida com os próximos episódios e temporadas em tempo real. Nenhuma intervenção humana é necessária durante todo o processo. Quando o download termina, o Sonarr move o arquivo para o local apropriado e renomeia o arquivo, se necessário.

**[Radarr](https://radarr.video/)** é exatamente a mesma coisa, mas para filmes.

## Pesquisar lançamentos automaticamente com indexadores Usenet e torrent

O Sonarr e o Radarr podem contar com duas maneiras diferentes de baixar arquivos: através de arquivos bin Usenet (grupos de notícias) ou através de torrents. Será configurado somente a opção Torrent utilizando o cliente Transmission Web.

## Indexadores de torrents com Prowlarr

Os arquivos torrents são pesquisados automaticamente pelo Sonarr/Radarr através de uma lista de indexadores que você deve configurar. Indexadores são APIs que permitem a busca de lançamentos específicos organizados por categorias. Pense em navegar no Pirate Bay programaticamente. É por isso que usaremos outra ferramenta chamada Prowlarr. É considerado como uma API de proxy local para os indexadores de torrent mais populares. Ele pesquisa e analisa informações de sites heterogêneos.



