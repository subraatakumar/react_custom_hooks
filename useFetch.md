```js
// App.js

import Users from "./components/Users"
import Products from "./components/Products"

const App = () => {

  return <>

    <Users />
  </>;
};

export default App;
```

```js
// useFetch.js
import React, {useState, useEffect} from 'react'

const useFetch = (api_url) => {
  const [datas, setDatas] = useState([]);
  const [error, setError] = useState("");
  const [loading, setLoading] = useState(false);

  useEffect(() => {
    setLoading(true);
    fetch(api_url)
      .then((res) => res.json())
      .then((json) => setDatas(json))
      .catch(e => {
        console.log("error")
        setError("Something went worng!")
      })
      .finally(() =>{
        setLoading(false);
      })

  }, []);

  return [datas, error, loading];
}

export default useFetch;
```

```js
// Products.js
import React, {useState, useEffect} from 'react';
import useFetch from "../custom_hooks/useFetch"


const Products = () => {
  const [datas, error, loading] = useFetch('https://fakestoreapi.com/products');

  if(loading){
    return(<p>Loading...</p>)
  }
  if(error.length > 0){
    return(<p>{error}</p>)
  }

  return <>
    {
      datas.map((data, index) => <p key={index}>{data?.title}</p>)
    }
  </>;
};

export default Products;
```

```js
// Users.js
import React, {useState, useEffect} from 'react';
import useFetch from "../custom_hooks/useFetch"


const Users = () => {
  const [datas, error, loading] = useFetch('https://fakestoreapi.com/users');

  if(loading){
    return(<p>Loading...</p>)
  }
  if(error.length > 0){
    return(<p>{error}</p>)
  }

  return <>
    {
      datas.map((data, index) => <p key={index}>{data?.username}</p>)
    }
  </>;
};

export default Users;
```
