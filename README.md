# Ciencia-de-dados-na-IOT

~~~ java script
//Abrindo o dataset utilizado
var img = ee.Image('COPERNICUS/S2_SR/20210109T185751_20210109T185931_T10SEG');

// Dividindo a em duas bandas a imagem
var swir1 = img.select('B11');
var swir2 = img.select('B12');
Map.setCenter(-122.276, 37.456, 12);

Map.addLayer(swir1, {min: 1500, max: 3000}, 'swir1');
Map.addLayer(swir2, {min: 0, max: 1500}, 'swir2');
var aspect = ee.Terrain.aspect(img);

// Converte para radianos e faz o seno e cosseno.
var sinImage = aspect.divide(180).multiply(Math.PI).sin();
var cosImage = aspect.divide(180).multiply(Math.PI).cos();


//Coloca uma camada do seno e do cosseno
Map.addLayer(sinImage, {min: -1, max: 1}, 'sin');
Map.addLayer(cosImage, {min: -1, max: 1}, 'cos');

// faz a adição das duas bandas da imagem
var addition = swir1.add(swir2);
Map.addLayer(addition, {min: 100, max: 600}, 'addition');

// faz a subtração das duas bandas da imagem
var subtraction = swir1.subtract(swir2);
Map.addLayer(subtraction, {min: 0, max: 500}, 'subtraction');

// faz a multiplicação das duas bandas da imagem
var multiplication = swir1.multiply(swir2);
Map.addLayer(multiplication, {min: 2e2, max: 9e2}, 'multiplication');

// faz a divisão das duas bandas da imagem
var division = swir1.divide(swir2);
Map.addLayer(division, {min: 0, max: 2}, 'division');
~~~
