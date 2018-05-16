# install Axios for http request to fetch data

  move to projecdt folder 

    /Projs/albums 
    
    npm install --save axios
  
  
    axios will be install inside /albums/node_modules/Axios
  
  
    example usage
      axios.get('https://rallycoding.herokuapp.com/api/music_albums')
        .then(response => console.log(response));

 this is just like the AFHTTPSessionManager in iOS with call backs when complete so it doesn't block the main thread
 when loading.
 
 
 
             {data: Array(5), status: 200, statusText: undefined, headers: {…}, config: {…}, …}
            config:{adapter: ƒ, transformRequest: {…}, transformResponse: {…}, timeout: 0, xsrfCookieName: "XSRF-TOKEN", …}
            data:(5) [{…}, {…}, {…}, {…}, {…}]
            headers:{x-content-type-options: "nosniff", server: "Cowboy", connection: "keep-alive", x-rack-cors: "preflight-hit; no-origin", vary: "Origin", …}
            request:XMLHttpRequest {UNSENT: 0, OPENED: 1, HEADERS_RECEIVED: 2, LOADING: 3, DONE: 4, …}
            status:200
            statusText:undefined
            __proto__:Object
