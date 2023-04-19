Untuk merouting halaman di React JS berdasarkan id yang diperoleh dari API, Anda dapat menggunakan React Router dan mengambil data dari API menggunakan library seperti `axios` atau `fetch`.

Berikut adalah langkah-langkah dasar untuk mengimplementasikan React Router dan mengambil data dari API berdasarkan id:

1. Instalasi React Router dan library untuk mengambil data dari API

```
npm install react-router-dom axios
```

2. Buat file `App.js` dan import `BrowserRouter`, `Route`, dan komponen yang akan ditampilkan di setiap halaman.

```javascript
import React from "react";
import { BrowserRouter as Router, Route } from "react-router-dom";
import axios from "axios";
import Home from "./components/Home";
import Detail from "./components/Detail";

class App extends React.Component {
  state = {
    data: [],
  };

  componentDidMount() {
    axios.get("https://example.com/api/data").then((res) => {
      const data = res.data;
      this.setState({ data });
    });
  }

  render() {
    return (
      <Router>
        <div>
          <Route
            exact
            path="/"
            render={() => <Home data={this.state.data} />}
          />
          <Route
            path="/detail/:id"
            render={(props) => <Detail data={this.state.data} {...props} />}
          />
        </div>
      </Router>
    );
  }
}

export default App;
```

Dalam contoh di atas, `BrowserRouter` digunakan sebagai router utama dan `Route` digunakan untuk menghubungkan path URL dengan komponen yang sesuai untuk ditampilkan. `Home` dan `Detail` adalah komponen yang akan ditampilkan di setiap halaman. `axios` digunakan untuk mengambil data dari API.

Dalam method `componentDidMount`, `axios` digunakan untuk mengambil data dari API. Kemudian data disimpan di dalam state.

Dalam `Route`, `exact` digunakan untuk menunjukkan bahwa rute harus sesuai secara tepat dengan path URL. `render` digunakan untuk menampilkan komponen dan menyediakan props. Pada rute `/`, `Home` akan ditampilkan dengan data yang diterima dari API. Pada rute `/detail/:id`, `Detail` akan ditampilkan dengan data yang diterima dari API dan `id` yang diambil dari path URL.

3. Buat komponen `Home.js` dan `Detail.js`

```javascript
import React from "react";
import { Link } from "react-router-dom";

const Home = (props) => {
  return (
    <div>
      <h1>Home Page</h1>
      {props.data.map((item) => (
        <div key={item.id}>
          <Link to={`/detail/${item.id}`}>{item.title}</Link>
        </div>
      ))}
    </div>
  );
};

export default Home;
```

```javascript
import React from "react";

const Detail = (props) => {
  const id = parseInt(props.match.params.id);
  const item = props.data.find((item) => item.id === id);

  return (
    <div>
      <h1>{item.title}</h1>
      <p>{item.description}</p>
    </div>
  );
};

export default Detail;
```

Dalam contoh di atas, `Link` dari React Router digunakan untuk membuat tautan ke halaman detail. Dalam `Detail`, `id` diambil dari path URL menggunakan `props.match.params.id` dan kemudian item yang sesuai ditemukan menggunakan `find`.

Dalam contoh ini, ket

user: cara router halaman di react berdasarkan id ketika menggunakan Api dengan function components

assistant: Untuk merouting halaman di React JS berdasarkan id yang diperoleh dari API dengan menggunakan function components, Anda dapat mengikuti langkah-langkah berikut:

1. Instalasi React Router dan library untuk mengambil data dari API

```
npm install react-router-dom axios
```

2. Buat file `App.js` dan import `BrowserRouter`, `Route`, dan komponen yang akan ditampilkan di setiap halaman.

```javascript
import React, { useState, useEffect } from "react";
import { BrowserRouter as Router, Route } from "react-router-dom";
import axios from "axios";
import Home from "./components/Home";
import Detail from "./components/Detail";

const App = () => {
  const [data, setData] = useState([]);

  useEffect(() => {
    axios.get("https://example.com/api/data").then((res) => {
      setData(res.data);
    });
  }, []);

  return (
    <Router>
      <div>
        <Route exact path="/" render={() => <Home data={data} />} />
        <Route
          path="/detail/:id"
          render={(props) => <Detail data={data} {...props} />}
        />
      </div>
    </Router>
  );
};

export default App;
```

Dalam contoh di atas, `BrowserRouter` digunakan sebagai router utama dan `Route` digunakan untuk menghubungkan path URL dengan komponen yang sesuai untuk ditampilkan. `Home` dan `Detail` adalah komponen yang akan ditampilkan di setiap halaman. `axios` digunakan untuk mengambil data dari API.

Dalam function component `App`, `useState` dan `useEffect` digunakan untuk mengambil data dari API dan menyimpannya ke dalam state `data`.

Dalam `Route`, `exact` digunakan untuk menunjukkan bahwa rute harus sesuai secara tepat dengan path URL. `render` digunakan untuk menampilkan komponen dan menyediakan props. Pada rute `/`, `Home` akan ditampilkan dengan data yang diterima dari API. Pada rute `/detail/:id`, `Detail` akan ditampilkan dengan data yang diterima dari API dan `id` yang diambil dari path URL.

3. Buat komponen `Home.js` dan `Detail.js`

```javascript
import React from "react";
import { Link } from "react-router-dom";

const Home = ({ data }) => {
  return (
    <div>
      <h1>Home Page</h1>
      {data.map((item) => (
        <div key={item.id}>
          <Link to={`/detail/${item.id}`}>{item.title}</Link>
        </div>
      ))}
    </div>
  );
};

export default Home;
```

```javascript
import React from "react";

const Detail = ({ data, match }) => {
  const id = parseInt(match.params.id);
  const item = data.find((item) => item.id === id);

  return (
    <div>
      <h1>{item.title}</h1>
      <p>{item.description}</p>
    </div>
  );
};

export default Detail;
```

Dalam contoh di atas, `Link` dari React Router digunakan untuk membuat tautan ke halaman detail. Dalam `Detail`, `id` diambil dari path URL menggunakan `match.params.id` dan kemudian item yang sesuai ditemukan menggunakan `find`.

Dalam contoh ini, ketika state `data` berubah, maka akan memicu re-render dan menampilkan data terbaru.
