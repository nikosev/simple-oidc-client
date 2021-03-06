# simple-oidc-client
A simple OpenID Connect (OIDC) client for browser-based JavaScript applications

## Simple OIDC Client - setup

You can either clone repo from github or download the project from releases.

### Clone repo

First we need to install apache, node.js and npm

```
sudo apt-get update
sudo apt-get install apache2
sudo apt-get install nodejs
sudo apt-get install npm
```
Then open a terminal and clone the repo to this directory:

```
cd /var/www/html
git clone https://github.com/rciam/simple-oidc-client.git
```

We use several third-party libraries to support our application:

```
jQuery
Bootstrap
oidc-client-js
```

We are going to install them with npm, the Node.js front-end package manager. In the terminal move in the `simple-oidc-client` folder:

```
cd simple-oidc-client
npm install jquery
npm install bootstrap
npm install oidc-client
```

By default, npm installs packages in the `node_modules` folder.

Important npm packages are usually not committed to source control. If you cloned the repository containing the final source code and want to restore the npm packages, open a command-line prompt in the `simple-oidc-client` folder and run `npm install` to restore packages.

We also create a basic `index.html` and a `popup.html` file.

We have two HTML files because `oidc-client-js` can open a popup to show the login form to the user.

### Download from releases

Install Apache and Node.js

```
sudo apt-get update
sudo apt-get install apache2
sudo apt-get install nodejs
```

Download the file from releases and extract it in apache home directory

```
cd /var/www/html
//TODO: change url and file name
wget releases.rar
tar releases.rar
```

## Simple OIDC Client - authentication

Now that we have everything we need, we can configure our login settings in `configuration.js`.

```
var settings = {
    title: 'Create Tokens',
    authority: 'https://localhost:8080',
    client_id: 'client',
    popup_redirect_uri: 'http://localhost/simple-oidc-client/popup.html',
    post_logout_redirect_uri: 'http://localhost/simple-oidc-client/index.html',
	
    response_type: 'id_token',
    scope: 'openid profile',
	
    debug: false,
    filterProtocolClaims: true
};
```

Let’s go quickly through the settings:

* `title` is the title on the navigation bar
* `authority` is the base URL of our IdentityServer instance. This will allow oidc-client to query the metadata endpoint so it can validate the tokens
* `client_id` is the id of the client we want to use when hitting the authorization endpoint
* `popup_redirect_uri` is the redirect URL used when using the signinPopup method. If you prefer not having a popup and redirecting the user in the main window, you can use the redirect_uri property and the signinRedirect method
* `post_logout_redirect_uri` is the redirect URL used when using the signoutRedirect method
* `response_type` defines in our case that we only expect an identity token back
* `scope` defines the scopes the application asks for
* `debug` displays user data
* `filterProtocolClaims` indicates to oidc-client if it has to filter some OIDC protocol claims from the response: nonce, at_hash, iat, nbf, exp, aud, iss and idp
	
Source: https://identityserver.github.io/Documentation/docsv2/overview/jsGettingStarted.html
