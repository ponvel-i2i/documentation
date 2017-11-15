## Getting Started

### Prerequisites

You're going to need:

 - **[Node JS](https://nodejs.org/en/)**

_Yes, that's it!_

### Getting Set Up

 1. Clone this repository to your hard drive with `git clone https://genivity.git.beanstalkapp.com/api-documentation.git`
 2. `cd api-documentation`
 3. To fetch Tapgenes documentation, `git fetch tapgenes-docs`
 4. To fetch Genivity documentation, `git fetch genivity-docs`
 5. To fetch Genivity Calculator documentation, `git fetch genivity-calc-docs`
 6. Install the dependencies: `npm install`
 7. Start the test server: `npm start`

Now go ahead and visit <http://localhost:4000> and you will be presented with a beautiful example API documentation as a starting point.

Go ahead and modify the markdown file at `source/index.md` to suit your needs.

### Publishing your API documentation

The easiest way to publish your API documentation is using this command within your `api-documentation` directory:

`npm run-script generate`

This will generate a `public` folder which you can upload anywhere you want.

> **Windows users:** You need to install the global `hexo-cli` package using `npm install -g hexo-cli`. To publish your API documentation under windows use `hexo generate`.

If you want other (more automated) deployment options like **git**, **heroku**, **rsync** or **ftp** - please take a look at the [Hexo deployment documentation](https://hexo.io/docs/deployment.html).
