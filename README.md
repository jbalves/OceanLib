# OceanLib

Construindo apps em poucas linhas, uma biblioteca que reúne as melhores soluções em Android em um só lugar

![Ocean Library](http://nuvem.oceanmanaus.com/index.php/s/N617Kal4qnNOGJu/download)

# Download

Adiciona no **build.gradle** raiz do seu projeto

``` Gradle 

allprojects {
		repositories {
			...
			maven { url "https://jitpack.io" }
		}
	}
```


Adiciona no **build.gradle** da pasta **app** do seu projeto

``` Gradle 

dependencies {
   compile 'com.github.oceanbrasil:OceanLib:1.1.4'
}
```

# Recursos

- [Imagens](https://github.com/oceanbrasil/LibOcean/wiki/Imagens)
- [Requisições HTTP e JSON](https://github.com/oceanbrasil/OceanLib/wiki/Requisi%C3%A7%C3%B5es-HTTP-e-JSON)


# Como usar o Ocean Library?

Veja alguns exemplos de uso da bilbioteca

## [Imagens](https://github.com/oceanbrasil/LibOcean/wiki/Imagens)

Ocean Library possui suporte para execução e tratamento de imagens sincronizando com views e otimizando o carregamento quando for necessário trabalhar com imagens externas como URL's ou imagens locais como Uri's.

Todas as imagens são processadas de forma assíncrona, de forma que evite os famosos "gargalos" de memórias e as "travadinhas" do seu app quando estiver processando imagens, seja elas locais ou externas.

### Bitmap

Carregar um bitmap em um ImageView

**URL**

``` Java 
Ocean.glide(context)
             .load("http://revista.oceanmanaus.com/oceanbook/moodle2.jpg")
             .build(GlideRequest.BITMAP)
             .resize(width, height) // Tamanho em pixel
             .into(ImageView);
```

**Callback**

Delegar um observador para receber o bitmap da imagem quando ela estiver pronto para uso

``` Java 
Ocean.glide(context)
            .load("http://revista.oceanmanaus.com/oceanbook/moodle2.jpg")
            .build(GlideRequest.BITMAP)
            .resize(width, height) // Tamanho em pixel
            .addDelegateImageBitmap(new ImageDelegate.BitmapListener() {
                @Override
                public void createdImageBitmap(Bitmap imageBitmap) {
                     // Bitmap pronto para uso               
                }
            })
            .into(ImageView);
```

### Bytes

Carregar somente os bytes da imagem

**URI**

``` Java 
Ocean.glide(context)
             .load(Uri.parse("/sdcard/cats.jpg"))
             .build(GlideRequest.BYTES)
             .toBytes(WIDTH, HEIGHT); // Tamanho em pixel
```

**Callback** 

Delegar um observador para receber os bytes da imagem quando eles estiverem pronto para uso

``` Java 
Ocean.glide(context)
            .load(R.mipmap.ic_launcher)
            .build(GlideRequest.BYTES)
            .addDelegateImageBytes(new ImageDelegate.BytesListener() {
                @Override
                public void createdImageBytes(byte[] data) {
                                    
                }
            })
            .toBytes(WIDTH, HEIGHT); // Tamanho em pixel
```


[Ver mais exemplos](https://github.com/oceanbrasil/LibOcean/wiki/Imagens)

## [Requisições HTTP e JSON](https://github.com/oceanbrasil/OceanLib/wiki/Requisi%C3%A7%C3%B5es-HTTP-e-JSON)

Requisições HTTP do tipo POST E GET

**Como usar**

``` Java 
@Override
protected void onCreate(Bundle savedInstanceState){

    // Iniciando uma nova requisição
    Ocean.newRequest("http://servidor", callback);
}

Request.RequestListener callback = new Request.RequestListener() {
    @Override
    public void onRequestOk(String response, JSONObject jsonObject, int error) {

    }
}
```

**POST**

``` Java 
Ocean.newRequest("http://servidor", callback)
.post()
.add("par1", "valor1")
.add("par2", 1)
.add("parN", 1.0f)
.send();
```

**GET**

``` Java 
Ocean.newRequest("http://servidor", callback).get().send();
```

**Upload de arquivos**

``` Java 
@Override
protected void onCreate(Bundle savedInstanceState){

    // Implementacao para recuperar o arquivo

    byte[] bitMapData; // Converter o arquivo para recuperar os bytes

    HashMap<String, byte[]> file = new HashMap<>();
    file.put("file.png", bitMapData);

    Ocean.newRequest("http://localhost/servidor", callback)
            .post()
            .add("file", file)
            .send();
}
```
