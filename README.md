# JS code to connect MetaMask to a webpage

This tutorial shows you the basic JS code needed to connect a webpage to MetaMask, use it to develop your dApp!

Serve the webpage and see how it works.

<h2>This repository contains:</h2>
<ol>index.html - Content and structure of the webpage</ol>
<ol>style.css - Styling of the webpage</ol>

<h2>How to run and serve the page</h2>

To serve the webpage, you can use a simple node server. Follow these instructions:
<ol>1 - Install Node.js - <a href="https://nodejs.org/en/download/">Download and instructions</a>.</ol>
<ol>2 - Install lite-server (with NPM in a terminal/command prompt).</ol>
  
  ```
  npm install -g lite-server 
  ```
  
  Now, you have the tools to serve a webpage on localhost.
  
  
  <ol>1 - Create a new folder and save the files from this project in it.</ol>
  <ol>2 - Serve the webpage via terminal/command prompt from the directory that has <code>index.html</code> in it and run:</ol>
 
 ```
 lite-server
 ```
 Now, your webpage will be available on http://127.0.0.1:3000/.
 
 <h2>The JS code</h2>
In this case, there is no separate .js file as the code is very simple.

This line retrieves the ethers.js library without having to install any dependencies.
<p></p>

```
<script src="https://cdn.ethers.io/lib/ethers-5.2.umd.min.js" type="application/javascript"></script>
```
<p></p>
Then the <code>connect()</code> function does the magic, retrieves the MetaMask accounts and prompt the user to connect to the page. 
<p></p>

```
async function connect() {

    // Identify the provider
    const provider = new ethers.providers.Web3Provider(window.ethereum, "any");

    // Prompt user for account connection
    await provider.send("eth_requestAccounts", []);

    // define the address signing the transactions (account selected)
    const signer = provider.getSigner();
    console.log("Account:", await signer.getAddress());
}
```

Use this as a base to create your decentralized application.

![image](https://user-images.githubusercontent.com/99700157/171196725-6e1db369-b210-44fc-b58c-a0bd8faad98b.png)
