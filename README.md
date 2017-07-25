This project is example of Create React App dynamically importing/loading ESRI API library.

[Live Example](https://ziveo.github.io/React-Dynamic-Import-ESRI-JS-API/)

```jsx harmony
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

let esriApi = '3.21';

class App extends Component {
  constructor() {
    super();

    this.state = {
      stylePath: null
    }
  }

  loadMap = () => {
    import('./import-modules/EsriLoader')
        .then(({bootstrap, dojoRequire}) => {
          bootstrap((err) => {
            if (err) {
              console.error(err);
            } else {
              this.setState({stylePath: `https://js.arcgis.com/${esriApi}/esri/css/esri.css`});
              dojoRequire(
                  [
                    'esri/map'
                  ],
                  (Map) => {
                    let map = new Map('mapMount', {
                      center: [-100, 30],
                      zoom: 4,
                      basemap: 'gray'
                    });
                    window.map = map;

                  });
            }
          }, {
            url: `https://js.arcgis.com/${esriApi}/`
          });
        })
        .catch(err => {
          // Handle failure
        });
  };

  render() {
    return (
      <div className="App">
        <div className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h2>React JS – Dynamically Importing ESRI JS API</h2>
        </div>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
        <button onClick={this.loadMap}>Load Map</button>
        <div id="mapMount"/>
        <link rel="stylesheet" type="text/css" href={this.state.stylePath} />
      </div>
    );
  }
}

export default App;
``` 

[logo]: https://raw.githubusercontent.com/ziveo/React-Dynamic-Import-ESRI-JS-API/gh-pages/ziveo.github.io-React-Dynamic-Import-ESRI-JS-API.png "React JS – Dynamically Importing ESRI JS API"
![alt text][logo]