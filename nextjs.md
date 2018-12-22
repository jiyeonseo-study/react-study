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

