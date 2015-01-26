Webpack Gotchas!
----------------

If you are coming from browserify or require.js, you probably know what are module bundlers, but if you do not know what are those, don't try to learn them, it's better that way. Some concepts are identical, but it'll confused you.

##What is Webpack

> **webpack** is a **module bundler**.

> webpack takes modules with dependencies and generates static assets representing those modules.

*If the above doesn't make sense yet, you can google it or just go on, you'll learn it along the way*

**References**

(What is Webpack?)[http://webpack.github.io/docs/what-is-webpack.html]

**If you are stupid**

If you are stupid just like me and cannot make sense of what you have just read on the online documentation of webpack. The following might help you, these are real life gotchas that you probably have encountered before.

###Gotcha no. 1 (what webpack does?)

**The Problem:**

You are developing an application using server side language (e.g. php), lets say it has 5 pages. Now you need to handle the client-side assets (i.e. images, stylesheets, javascript). Your application contains different features, like modal boxes, tables, gallery grid. These features are unique to each page. It's time to deploy the app, and you want it to be as fast as possible, the problem is:

      <link rel="stylesheet" href="public/styles/modal.css">
      <link rel="stylesheet" href="public/styles/gallery-grid.css">
      <link rel="stylesheet" href="public/styles/user-table.css">
    </head>
    <body>
      ...
      ...
      <script src="public/scripts/modal.js"></script>
      <script src="public/scripts/gallery-grid.js"></script>
      <script src="public/scripts/user-table.js"></script>
    </body>

Do you see my point, having your server requests all these assets all at once is a terrible idea.

**The Solution:**

You are an awesome php developer, and this is a no brainer, you'll only just have to render each "page" along with its assets dependency.

Like so:
      
    $css = array(
      'normalize.css',
      'main.css'
    );

    $js = (
      'jquery.js',
      'main.js'
    );

    $this->view->render(array('js' => $js, 'css'=>$css), 'home');

That is a gist from a little php framework when I was in 1st year college, but I suppose you get the point. **You require a dependency on demand**.

You have `rendered` the html page that would only have the dependency you declared for a specific view. (wise?). It's just templating.

That is possible, because you can render the view server side before sending it to the user/client. (full page reload).

**So what?**

This is possible using Webpack and even better, in webpack, it's so clever that it generates **common chunks** (these are source files that are shared among views or entry points ), and this is their concept of **code-splitting**. That is not all, but you should get the point of Webpack as a bundler.

