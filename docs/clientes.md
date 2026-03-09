# Acesso desde o QGIS

Esta secção ilustra como aceder a dados publicados em OGC API, através da aplicação cliente [QGIS](https://qgis.org/).

A lista de clientes que podem aceder a dados publicados em OGC API pode ser consultada nos repositórios de GitHub de cada Standard (por exemplo, [OGC API - Features](https://github.com/opengeospatial/ogcapi-features/tree/master/implementations/clients)) e inclui aplicações como LeafLet, OpenLayers, GDAL ou ArcGIS.

!!! info
    
    Para as demonstrações abaixo, foi usada a LTR do QGIS, que no momento em que este manual foi escrito é a 3.40.6. Mais detalhes podem ser consultados na tabela abaixo:

    <table width='100%' align='center'><tr><td>QGIS version</td><td>3.40.6-Bratislava</td></tr><tr><td>QGIS code revision</td><td><a href="https://github.com/qgis/QGIS/commit/5d7f6a3e265">5d7f6a3e265</a></td></tr><tr><td colspan="2">&nbsp;</td></tr><tr><td colspan="2"><b>Libraries</b></td></tr><tr><td>Qt version</td><td>5.15.13</td></tr><tr><td>Python version</td><td>3.12.3</td></tr><tr><td>GDAL version</td><td>3.8.4</td></tr><tr><td>PROJ version</td><td>9.4.0</td></tr><tr><td>EPSG Registry database version</td><td>v11.004 (2024-02-24)</td></tr><tr><td>GEOS version</td><td>3.12.1-CAPI-1.18.1</td></tr><tr><td>SQLite version</td><td>3.45.1</td></tr><tr><td>PostgreSQL client version</td><td>16.8 (Ubuntu 16.8-0ubuntu0.24.04.1)</td></tr><tr><td>SpatiaLite version</td><td>5.1.0</td></td></tr><tr><td>QWT version</td><td>6.1.4</td></tr><tr><td>QScintilla2 version</td><td>2.14.1</td></tr><tr><td>OS version</td><td>Ubuntu 24.04.2 LTS</td></tr><tr><td colspan="2">&nbsp;</td></tr></table>

## OGC API - Features

Para adicionar um layer do tipo "OGC API - Features", pode ser utilizado o browser do lado esquerdo, carregando no item "WFS/OGC API - Features" para chamar o context menu, e escolhendo "Nova Ligação". 

![OAF 1](img/oaf1.png)

No passo seguinte, é aberta uma caixa de configuração para introduzir os dados da ligação. Na secção `url` deve ser introduzido o url da Landing Page da OGC API: [https://ogcapi.dgterritorio.gov.pt/](https://ogcapi.dgterritorio.gov.pt/).

![OAF 2](img/oaf2.png)

!!! tip
    
    Opcões de WFS: para não sobrecarregar o QGIS e o servidor, recomenda-se estabelecer um número máximo de features, especialmente numa fase de exploração dos dados. Esse número pode ser sempre incrementado, se necessário. Para um número máximo de features de `100`, com uma paginação de `25`, o QGIS fará quatro pedidos ao servidor até satisfazer a quota máxima estabelecida de features; neste caso, 100.

Ao pressionar `ok` para fechar a caixa anterior, uma nova ligação aparecerá listada debaixo da secção "WFS/OGC API - Features", no browser panel. Ao carregar nesse item para expandir-lo irão aparecer todas as colecções de OGC API - Features, disponíveis no servidor.

![OAF 6](img/oaf6.png)

Qualquer uma destas colecções pode ser adicionada ao QGIS como layer, fazendo duplo click, ou carregando nela para chamar o menu de contexto e escolhendo "Add layer to project".

!!! tip
    
    Para não sobrecarregar o QGIS e o servidor, recomenda-se aplicar filtros a coleções OGC API - Features **antes de carregar a colecção**. No caso de quereremos filtrar por um determinado atributo, podemos carregar no botão `build query` para construir o filtro. Se tivermos interesse por uma determinada área, a recomendação é de fazer zoom para a área de interesse **antes de carregar a colecção** e seleccionar a checkbox "Only select features overlaping the view extent". 
    
    ![OAF 7](img/oaf7.png)

![OAF 4](img/oaf4.png)

!!! tip
    
    As colecções OGC API - Features também podem ser adicionadas através do top menu "Layer", escolhendo "Add Layer" e "Add WFS/OGC API - Features Layer".

    ![OAF 5](img/oaf5.png)

## OGC API - Tiles

O QGIS permite adicionar tiles vectoriais com o formato OGC API - Tiles. No browser panel do lado esquerdo, carregar no item "Vector Tiles" para chamar o context menu e seleccionar "New generic connection".

![OAT 3](img/oat3.png)

Na caixa de configuração deve-se indicar qual é o "source url" da colecção.

!!! tip
    
    Para obter "source url" da colecção pode-se consultar o endpoint de tileset metadata. Depois de identificar a colecção de interesse, através do [endpoint de colecções](https://ogcapi.dgterritorio.gov.pt/collections), carregar nessa colecção para obter a página da colecção. Por exemplo, se quiseremos os metadados de colecção de "CAOP2025 Municípios", podemos carregar nesse link que nos leva até: [https://ogcapi.dgterritorio.gov.pt/collections/municipios](https://ogcapi.dgterritorio.gov.pt/collections/municipios). A última parte do url - `municipios`- é o nome da colecção.

    Para aceder ao tileset metadata, podemos substituir o `NOME` neste url, por `municipios`:

    [https://ogcapi.dgterritorio.gov.pt/collections/NOME/tiles/WebMercatorQuad/metadata](https://ogcapi.dgterritorio.gov.pt/collections/municipios/tiles/WebMercatorQuad/metadata)

    Acedendo a url podemos consultar o Tile URL template. 

    ![OAT 1](img/oat1.png)

    Podemos copiar este valor para o "source url" do QGIS, substituindo `tileMatrix` por `z`, `tileRow` por `y` e `tileCol` por `x`: 

    ![OAT 2](img/oat2.png)

Depois de aceitar esta configuração, a colecção irá aparecer listada debaixo do item "Vector Tiles". Ela pode ser adicionada ao mapa, carregando para obter o context menu, e depois seleccionando "Add layer to project".

![OAT 4](img/oat4.png)

## OGC API - Maps

Para acceder a colecções disponibilizadas como OGC API - Maps, começamos por identificar o endpoint da colecção através do [endpoint de colecções](https://ogcapi.dgterritorio.gov.pt/collections?f=html). Por exemplo para o tema "OrtoSat 30 cm - Portugal Continental - 2023 (Cor Verdadeira)":

* [https://ogcapi.dgterritorio.gov.pt/collections/ortos-rgb](https://ogcapi.dgterritorio.gov.pt/collections/ortos-rgb)

Através do menu "Layer", seleccionar a opção "Add Layer" e "Add Raster Layer".

![OAM 1](img/oam1.png)

 Na caixa de configuração, seleccionar o radio button "OGC API", que irá expandir um menu com opções de configuração.

![OAM 2](img/oam2.png)

Na secção "OGC API - endpoint", deve-se preencher o url da colecção que identificámos acima e na `API`, escolher `map`. Todas as outras configurações são opcionais. Depois de aceitar esta configuração, a colecção será adicionada ao mapa.

![OAM 3](img/oam3.png)

## OGC API - Records

Actualmente a DGT disponibliza duas colecções como OGC API - Records: o "Sistema Nacional de Informação Geográfica - SNIG" e o "Portal de Informação Territorial - PoInT". Os respectivos endpoints podem ser identificados [endpoint de colecções](https://ogcapi.dgterritorio.gov.pt/collections).

Para visualizar uma coleção OGC API - Records no QGIS, podemos utilizar o core plugin [MetaSearch](https://docs.qgis.org/3.40/en/docs/user_manual/plugins/core_plugins/plugins_metasearch.html), que já vem por defeito com a instalação do QGIS. É possível aceder ao plugin, através da opção "Web->MetaSearch->MetaSearch" no top level menu.

![OAREC 1](img/oarec1.png)

Carregar no botão `new` para adicionar um novo endpoint de Records, e na caixa de configuração, adicionar o url que identificámos na página de colecções.

![OAREC 2](img/oarec2.png)

Ao pressionar `Ok`, este endpoint será adicionado á lista, e podemos carregar no botão `service info`, para obter informações sobre este serviço.

![OAREC 3](img/oarec3.png)

!!! warning
    
    O QGIS poderá demorar algum tempo a fazer a comunicação, e perguntar ao utilizador se que esperar ou interromper o processo; para continuar, escolha esperar.

Na tab `search` temos a possibilidade de listar os registos do catálogo e aplicar filtros, por bounding box ou palavra chave.

![OAREC 4](img/oarec4.png)

Carregue num registo para visualizar o seu conteúdo.

![OAREC 5](img/oarec5.png)
