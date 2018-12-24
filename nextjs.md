# Next.js 

## Tutorials 
- [https://nextjs.org/learn/](https://nextjs.org/learn/)

## Why 
- Server-rendered by default
- Automatic code splitting for faster page loads
- Simple client-side routing (page based)
- Webpack-based dev environment which supports (HMR)
- Able to implement with Express or any other Node.js HTTP server
- Customizable with your own Babel and Webpack configurations

## Getting started
### package.json 
```
{
  "name": "hello-next",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "next",
    "build": "next build",
    "start": "next start"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "next": "^7.0.2",
    "react": "^16.6.3",
    "react-dom": "^16.6.3"
  }
}
```

```
npm run dev
```

[http://localhost:3000/](http://localhost:3000/)

### Route
root : `pages/index.js` 

/about : `pages/about.js` 

### Error Handling 

### Link 
```
import Link from "next/link";

<Link href="/about">
  <a>About Page</a>
</Link>
```
`next/link` does all the  handling for you.

```
import {withRouter} from 'next/router'

const Page = withRouter((props) => (
    <Layout>
       <h1>{props.router.query.title}</h1>
       <p>This is the blog post content.</p>
    </Layout>
))
```

- `?title=ThisIsParam` => `{props.router.query.title}` : `ThisIsParam`

```
import {withRouter} from 'next/router'
import Layout from '../components/MyLayout.js'

const Content = withRouter((props) => (
  <div>
    <h1>{props.router.query.title}</h1>
    <p>This is the blog post content.</p>
  </div>
))

const Page = (props) => (
    <Layout>
       <Content />
    </Layout>
)

export default Page
```

### as 
```
 <Link as={`/p/${props.id}`} href={`/post?title=${props.title}`}>
      <a>{props.title}</a>
    </Link>
```
- it uses `history API`. 

## Fetching Data
### server-rendered, getInitialProps
```
const Index = props => {
  ...
}
Index.getInitialProps = async function() {
  const res = await fetch("https://api.tvmaze.com/search/shows?q=batman");
  const data = await res.json();

  console.log(`Show data fetched. Count: ${data.length}`);

  return {
    shows: data
  };
};

export default Index;

```
- server-rendered, so the console log is shown only on the server. 

### Fetch Data in Client Side, getInitialProps
```
Post.getInitialProps = async function (context) {
  const { id } = context.query
  const res = await fetch(`https://api.tvmaze.com/shows/${id}`)
  const show = await res.json()

  console.log(`Fetched show: ${show.name}`)

  return { show }
}
```

- `context` 
- [data fetching doc](https://github.com/zeit/next.js#fetching-data-and-component-lifecycle) 

## Style

```
<style jsx>
  h1, a {
    font-family: "Arial";
  }

  ul {
    padding: 0;
  }

  li {
    list-style: none;
    margin: 5px 0;
  }

  a {
    text-decoration: none;
    color: blue;
  }

  a:hover {
    opacity: 0.6;
  }
</style>
```

- to use any dynamic variable inside styled-jsx
- That is why CSS needs to go inside of a template string. ({``}) 
- CSS rules have no effect on elements inside of a child component.
  - or [global selectors](https://github.com/zeit/styled-jsx#one-off-global-selectors)
```
 <style jsx global>{`
      .markdown {
        font-family: "Arial";
      }

      .markdown a {
        text-decoration: none;
        color: blue;
      }

      .markdown a:hover {
        opacity: 0.6;
      }

      .markdown h3 {
        margin: 0;
        padding: 0;
        text-transform: uppercase;
      }
    `}</style>
```
- more detailed from https://github.com/zeit/styled-jsx 

## Deploy
- [Zeit Now](https://zeit.co/now)

```
// package.json
"scripts": {
  "start": "next start -p $PORT"
}

$ PORT=8000 npm start
```

### install Now
```
npm install -g now
```
more details - https://zeit.co/docs/v2/getting-started/installation/ 

### new file `now.json` 
```
{
  "version": 2,
  "builds": [{ "src": "package.json", "use": "@now/next" }]
}

$ now 
$ npm run build // deploy the app with the `.next` directory.
```
port 443 (the default port for "https" websites)

## export
create file `next.config.js` in the root path.

```
module.exports = {
  exportPathMap: function () {
    return {
      '/': { page: '/' }
    }
  }
}
```
- Next.js to export only the index (/) page. 

add on `package.json`
```
"scripts": {
    "export": "next export"
}
```

- `npm run build && npm run export` 
- exported HTML content in path `out/`
- `cd out` and `serve -p 8080` with [serve](https://www.npmjs.com/package/serve) 

- to export other pages 
```
module.exports = {
  exportPathMap: function () {
    return {
      '/': { page: '/' },
      '/about': { page: '/about' },
      '/p/hello-nextjs': { page: '/post', query: { title: 'Hello Next.js' } },
      '/p/learn-nextjs': { page: '/post', query: { title: 'Learn Next.js is awesome' } },
      '/p/deploy-nextjs': { page: '/post', query: { title: 'Deploy apps with Zeit' } }
    }
  }
}
```
