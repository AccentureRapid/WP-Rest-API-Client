A WordPress REST API client for Angular
==========================================

This a AngularJS client using  [WordPress REST API](http://wp-api.org/).  It is under active development, and should be considered beta version. More features are in progress.

It is designed and tested to work with WP-API v2.

**Index**:
[Purpose](#purpose) &bull;
[Installation](#installation) &bull;
[Using The Client](#using-the-client) &bull;
[Authentication](#authentication) &bull;

## Purpose
This client is designed to make it easy for your [AngularJS](https://angularjs.org) application to request resources from WordPress with WP-API v2.

## Installation
To use the library, download lib/wp_services.js and you can rename it if you like.

## Using The Client
You need include the WPSerive.
```javascript
var myApp = angular.module('myApp', ['WPSerive']);

// set the baseURL of WordPress
myApp.config(['WPConfig',
	function(WPConfig) {
		WPConfig.baseURL = 'http://localhost/wordpress/';
	}
]);
```

We support requesting posts using  promise-style syntax:
```javascript
// Promises
WP.posts().fetchAllPosts(data).then(function(data) {
	// do something with the returned posts
}, function() {
	// handle error
});
```

### Handle Posts

To get posts, use the `.posts()` method to get the serivce of WPPOsts, which is incharge of the handle of posts.

```js
WP.posts().fetchAllPosts(data).then(function(data) {
	$scope.posts = data;
}, function() {
	console.error('Error while query posts');
});
```

Additional methods provided, by endpoint:
* **posts**
    - `wp.posts().fetchAllPosts()`: get a collection of posts (default query)
    - `wp.posts().id( n )`: get the post with ID *n*
    - `wp.posts().update( post )`: update the post		
* **users**
    - `wp.users().fetchAllUsers()`: get a collection of users (default query)
    - `wp.users().id( n )`: get the user with ID *n*

following is in progress
* **pages**
* **types**
* **media**

## Authentication

You must be authenticated with WordPress to create, edit or delete resources via the API.
This library currently supports [basic HTTP authentication](http://en.wikipedia.org/wiki/Basic_access_authentication). To authenticate with your WordPress install,

1. Download and install the [Basic Authentication handler plugin](https://github.com/WP-API/Basic-Auth) on your target WordPress site. *(Note that the basic auth handler is not curently available through the plugin repository: you must install it manually.)*
2. Activate the plugin.
3. Specify the username and password of an authorized user (a user that can edit_posts) when instantiating the WP request object:
```javascript
myApp.config(['$httpProvider',
	function($httpProvider) {
		$httpProvider.interceptors.push('basicAuthInterceptor');
	}
]);

WPConfig.username = 'xxx';
WPConfig.password = 'xxx';
```





