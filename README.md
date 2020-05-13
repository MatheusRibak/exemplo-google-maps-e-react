# exemplo-google-maps-e-react

Este é um exemplo de como utilizar o Google Maps juntamente com o React. 
Ele foi postado originalmente no dev.to, caso queira acessar basta clicar aqui:

https://dev.to/matheusribak/ola-coleguinha-vamos-aprender-a-usar-a-api-google-maps-com-react-18h5

### Criando a Aplicação React e Instalando as dependências do Google Maps

Abra seu terminal e execute os comandos a seguir:

**Criando a Aplicação React:**

```
npm init react-app exemplo-google-maps-e-react
```

**Navegue até a pasta que foi criada e instale as dependências do Maps:**

```
cd exemplo-google-maps-e-react
npm install google-maps-react
```

### Realizando o import do Maps em nosso código

**Após ter feito as instalações abra o aplicativo e realize a seguinte importação para termos acesso ao Maps:**

```javascript
import { Map, GoogleApiWrapper } from 'google-maps-react';
```

### Adicionado o Maps ao nosso código

**Depois de ter feito a importação basta adicionar o seguinte código para adicionar o Maps ao código:**

```javascript
export class MapContainer extends Component {

  render() {
    return (

      <Map
        google={this.props.google}
        zoom={7}
        initialCenter={{ lat: -27.0922364, lng: -52.6166878 }}
      >
      </Map>

    );
  }
}
```

Podemos aqui definir algumas configurações do maps, em meu exemplo eu uso:

**zoom:** Irá definir o zoom que o mapa irá ter ao ser carregado em tela;

**initialCenter:** Irá Definir qual a latitude e longitude inicial do mapa, neste caso optei pela cidade de Chapecó-SC.

**Após isto ainda precisamos realizar o export do que criamos acima e informar uma key para o google maps.**

```javascript
export default GoogleApiWrapper(
  (props) => ({
    apiKey: 'AQUI DEVE SER INFORMADA SUA KEY',
  }
))(MapContainer)
```

### Rodando a aplicação para ser o resultado:

**Para rodar a aplicação execute em seu terminal:**

```
npm start
```

**Você terá um resultado parecido com este:**

![alt text](https://raw.githubusercontent.com/MatheusRibak/exemplo-google-maps-e-react/master/googlemapsexemplo.png "Logo Title Text 1")

### Adicionando Marcadores em nosso mapa:

Algo muito utilizado em maps hoje em dia é a adição de marcadores no mesmo, para isso precisamos:

**Realizar a importação do "Marker":**

```javascript
import { Map, GoogleApiWrapper, Marker } from 'google-maps-react';
```

**Adicionando os lugares que devem ser marcados em nosso mapa:**

```javascript
  constructor(props) {
    super(props);

    this.state = {
      stores: [
        { latitude: -26.9853947, longitude: -52.603549, local: "Cordilheira Alta" },
        { latitude: -26.9605363, longitude: -52.5335505, local: "Xaxim" },]
    }
  }
```

Conseguimos definir a latitude e a longitude a serem marcadas em nosso mapa, o terceiro parâmetro é opcional e eu gosto de colocar para sabermos em qual lugar está o marcador através do console ou de um alert por exemplo. 

**Percorrendo os marcadores para criar a tag Marker:**

```javascript
  displayMarkers = () => {
    return this.state.stores.map((store, index) => {
      return <Marker key={index} id={index} position={{
        lat: store.latitude,
        lng: store.longitude
      }}
      />
    })
  }
```

**Adicionando os marcadores ao mapa:**

```javascript
  render() {
    return (

      <Map
        google={this.props.google}
        zoom={7}
        initialCenter={{ lat: -27.0922364, lng: -52.6166878 }}
      >

        {this.displayMarkers()}
      </Map>

    );
  }
```

Rodamos novamente a aplicação e vamos ter o seguinte resultado:

![alt text](https://raw.githubusercontent.com/MatheusRibak/exemplo-google-maps-e-react/master/marcadores.png "Logo Title Text 1")

