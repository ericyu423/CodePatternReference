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
