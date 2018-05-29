# Ng5Maps

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

Criar o ponteiro para o elmenento <div> definido no template HTML - vínculo feito pela variável 'gmap' no html #gmap
    
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
    
    Referenciar o arquivo javascript no arquivo index.html do projeto

### Passo 2:
    
    Criar um wrapper para a classe a ser utilizada 'MarkerClusterer'

    import { Component, OnInit, ViewChild } from '@angular/core';
    import { } from '@types/googlemaps';

    declare var MarkerClusterer: any;

E agora é só divertir usando os componentes do Google MarkerCLusterer no seu projeto....

    const markerCluster = new MarkerClusterer(this.map, markers,
      {imagePath: 'https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/m'}
    );
