# How to connect MetaMask to a webpage

This tutorial shows you the basic JavaScript code needed to connect a webpage to MetaMask; use it to develop your dApp!

In this case, we'll use the `window.ethereum` global API injected directly by MetaMask, but there are other ways to do it, using `ethers.js` or `web3.js`, for example.

You can find the reference code in the [MetaMask docs](https://docs.metamask.io/guide/ethereum-provider.html).

Serve the webpage and see how it works.

## This repository contains
* index.html - Content and structure of the webpage
* style.css - Styling of the webpage

## How to run and serve the page

To serve the webpage, you can use a simple node server. Follow these instructions:
1. Install Node.js - [Download and instructions](https://nodejs.org/en/download/).
1. Install lite-server (with NPM in a terminal/command prompt).
  
  ```sh
  npm install -g lite-server 
  ```
  
  Now, you have the tools to serve a webpage on localhost.
  
  
1. Create a new folder and save the files from this project in it.
1. Serve the webpage via terminal/command prompt from the directory that has <code>index.html</code> in it and run:

 ```
 lite-server
 ```
 Now, your webpage will be available on http://127.0.0.1:3000/.
 
## index.html

For this example, we start with an empty HTML boilerplate. Since we use the `window.ethereum` API injected by MetaMask, we don't need to import any library, but note that [MetaMask must be installed](https://metamask.io/download/)!

Start by creating a new `index.html` file in your project directory.

You can use the following boilerplate.

> Note that the file in the repository is linked to a `.css` stylesheet. The project works without the stylesheet, but it will look different than the images from this tutorial. Take the CSS code from the repository if you want the same styling.

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <!-- <link rel="stylesheet" type="text/css" href="./style.css"/> -->
  
    <title>Connect MetaMask</title>
</head>

<body>


</body>

</html>
```

I named the page `Connect MetaMask`.

Once the main file is created, let's add some basic HTML elements. We just add a few sentences to describe what the page does and a button to prompt the user to connect MetaMask.

Inside the `<body>` tag place:

```html

<div class="parent">
    <div class="div1">
        <h1 class="center">Connect MetaMask to a webpage</h1>
        <h2 class="center">This page shows you how to connect MetaMask to a webpage to create a DApp!</h2>
        <h3 class="center">Check the source code in the <a href="https://github.com/soos3d/connect-metamask-to-webpage" target="_blank">GitHub repo</a>.</h3>
        <p class="center">Click the button to prompt MetaMask to connect</p>
    </div>

    <div class="div2">
        <h3>Click the button to connect MetaMask to the website</h3>
        <button onclick="connect()">Connect Wallet</button>       <!-- The `onclick` event means we'll call the specified function when we click the button. -->
    </div>
</div>

```

> Note that the `class` tags refer to the CSS code included in the repo; the code still works without the stylesheet; it just looks different.

At this point, we can already serve the page and run `lite-server` in the terminal from the folder where the `index.html` file lives. 
Now that our HTML skeleton is ready, we can work on the connection itself; you won't believe how easy it is!
It will look like this:

![screely-1662992658813](https://user-images.githubusercontent.com/99700157/189679235-cb2cd12d-4a28-41c4-803a-07129580647c.png)

## Connect MetaMask to the webpage

Now that our HTML skeleton is ready, we can work on the connection itself; you won't believe how easy it is!

To prompt the user to connect their MetaMask to the page, we'll use some simple JavaScript code, and we can place it in a `<script>` tag inside the HTML body. This is excellent for testing and learning, but you should use a separate `.js` file for more complex apps. 

> Make sure to name the function the way you specified in the `onclick` event on the HTML button.

```html
<script>
  
 // Identify the accounts and connect MetaMask to the website.
 function connect() {
     ethereum.request({
         method: 'eth_requestAccounts'     // Use the eth_requestAccounts method to promt the user to select and connect an account.
      
      // Log and error in the console if the user refuses the connection. 
     }).then(handleAccountsChanged).catch((error) => {    
         if (error.code === 4001) {
             // EIP-1193 userRejectedRequest error
             console.log('Please connect to MetaMask.');
         } else {
             console.error(error);
         }
     });
 }
</script>
```

That's it! Now you can connect MetaMask to this webpage! The reference code can be found in the [MetaMask docs](https://docs.metamask.io/guide/rpc-api.html#restricted-methods).

At this point, the HTML file should look like this:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" type="text/css" href="./style.css" />
    <title>Connect MetaMask</title>
</head>

<body>
    <div class="parent">
        <div class="div1">
            <h1 class="center">Connect MetaMask to a webpage</h1>
            <h2 class="center">This page shows you how to connect MetaMask to a webpage to create a DApp!</h2>
            <h3 class="center">Check the source code in the <a href="https://github.com/soos3d/connect-metamask-to-webpage" target="_blank">GitHub repo</a>.</h3>
            <p class="center">Click the button to prompt MetaMask to connect</p>
        </div>

        <div class="div2">
            <h3>Click the button to connect MetaMask to the website</h3>
            <button onclick="connect()">Connect Wallet</button>
        </div>
    </div>

    <script>
        // Identify the accounts and connect MetaMask to the website.
        function connect() {
            ethereum
                .request({
                    method: 'eth_requestAccounts'
                })
                .then(handleAccountsChanged)
                .catch((error) => {
                    if (error.code === 4001) {
                        // EIP-1193 userRejectedRequest error
                        console.log('Please connect to MetaMask.');
                    } else {
                        console.error(error);
                    }
                });
        }
    </script>

</body>

</html>
```

### Add more functionality

Altough this code allows us to already connect the page to MetaMask, we can add some functionality. For example, promt the user to switch to the network used by our DApp.



Use this as a base to create your decentralized application.

![image](https://user-images.githubusercontent.com/99700157/171196725-6e1db369-b210-44fc-b58c-a0bd8faad98b.png)
