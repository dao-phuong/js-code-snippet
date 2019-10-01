# js-code-snippet

## fetch image with base64 type

### XMLHttpRequest
```
  fetchImage = (url) => {
    return new Promise((resolve, reject) => {
      const XMLHttpRequest = window.XMLHttpRequest;
      const request = new XMLHttpRequest();
      request.open('GET', url, true);
      request.responseType = "arraybuffer";

      request.onload = (event) => {
        let arrayBuffer = request.response;
        let binary = '';

        if (arrayBuffer) {  
          let bytes = new Uint8Array(arrayBuffer);
          let len = bytes.byteLength;
          for (let i = 0; i < len; i++) {
              binary += String.fromCharCode( bytes[ i ] );
          }
        }

        const base64Result = window.btoa( binary );
        resolve(`data:image/jpeg;base64, ${base64Result}`);
      }

      request.send(null);
    });
  }

```

### fetchApi
```
  fetchImagev2 = (url) => {
    return new Promise((resolve, reject) => {
      fetch(url)
        .then(response => response.arrayBuffer())
        .then(response => {
          let binary = '';
          if (response) {  
            let bytes = new Uint8Array(response);
            let len = bytes.byteLength;
            for (let i = 0; i < len; i++) {
                binary += String.fromCharCode( bytes[ i ] );
            }
          }

          const base64Result = window.btoa( binary );
          resolve(`data:image/jpeg;base64, ${base64Result}`);
        });
    });
  }
```
