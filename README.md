# Ng5Maps - Google Maps API & Google Maps MarkerClusterer

Utilizando API nativa do Google Maps em projeto Angular 5.x

## Preparando o projeto

Alterar o index.html e incluindo a referência conforme documentação do google.maps, como URL no head:

    <head>

        <meta charset="utf-8">
        <title>Ng5Maps</title>
        <base href="/">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        ...
        <script src="https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/markerclusterer.js"></script>
        <script type="text/javascript" src="https://maps.googleapis.com/maps/api/js?key=API_KEY&libraries=places"></script>

    </head> 

## Install Google Maps types for typescript support

Executar o comando:

    npm install — save @types/googlemaps


## Implementar no componente

### No template HTML

Declarar a div que irá receber o google maps

    <div #gmap style="width:100%;height:430px; margin-top:0.5%"></div>

** Note que #gmap define uma variável para receber a referência do elemento <div>

### No componente TypeScript

Importar os typings do google maps

    import { } from '@types/googlemaps';

Criar, **NO ARQUIVO TypeScript do componente em que será utilizado o GoogleMaps**, o ponteiro para o elemento <div> definido no template HTML - vínculo feito pela variável 'gmap' no html #gmap
    
    import { Component, OnInit, ViewChild } from '@angular/core';

    declare var MarkerClusterer: any;

    @Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: ['./app.component.css']
    })
    export class AppComponent implements OnInit {
    
    ...

    @ViewChild('gmap') gmapElement: any;
    map: google.maps.Map;

    ...


## Referenciar arquivo javascript (js) externo, sem os wrappers para typescript

### Passo 1:

#### Opção 1 - Utilizando a referência da URL pública onde está o javascript (neste caso, o CDN) 

Referenciar o arquivo javascript no arquivo index.html do projeto

Exemplo já mostrado anteriormente, observe a linha:

    <head>

        ...
        <script src="https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/markerclusterer.js"></script>
        ...

    </head>

A linha acima referencia no html um arquivo javascript publicado em uma url externa na internet. 

#### Opção 2 - Fazendo download do arquivo javascript para o projeto local, referenciando a este arquivo localmente

Para adicionar um arquivo javascript local, o procedimento é o mesmo, alterando apenas a origem do arquivo ou adicionando-o no arquivo '.angular-cli.json' para o webpack compilar no arquivo final.
    
    ...
    "scripts": [
        "local-do-arquivo/markerclusterer.js"
    ],
    ...


### Passo 2:

Criar, **NO ARQUIVO TypeScript do componente em que será utilizado o MarkerClusterer**, o objeto que representa a Classe do GoogleMaps que deseja utilizar: '**_declare var MarkerClusterer: any_**' (variável global, fora da classe do componente que a utiliza);

Criar um wrapper para a classe a ser utilizada 'MarkerClusterer'

    import { Component, OnInit, ViewChild } from '@angular/core';
    import { } from '@types/googlemaps';

    declare var MarkerClusterer: any;

    @Component({
        selector: 'app-root',
        templateUrl: './app.component.html',
        styleUrls: ['./app.component.css']
    })
    export class AppComponent implements OnInit {

**Atenção à linha acima: 'declare var MarkerClusterer: any;'**

E agora é só divertir usando os componentes do Google MarkerCLusterer no seu projeto....

    const markerCluster = new MarkerClusterer(this.map, markers,
      {imagePath: 'https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/m'}
    );

## Live Demos

[![Marker Clusterer Screenshot](https://googlemaps.github.io/js-marker-clusterer/screenshot.png)](https://googlemaps.github.io/js-marker-clusterer/docs/examples.html)