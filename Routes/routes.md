# Working with Routes in Vue StoreFront

We can use ``extendRoutes`` function ``nuxt.config.js`` to add/update routes in Vue StoreFront

This function takes two parameters names ``routes`` and ``resolve``. 

``routes`` : This hold an array of already registered routes, we can push, delete or updates entries from this array.
``resolve`` : helper function for resolving Vue.js components based on their paths in the project

## Adding a Route

````
// nuxt.config.js

export default {
    router: {
        extendRoutes(routes, resolve) {
           
          // Adding a new Route
          routes.push({
            name: 'CustomRoute',
            path: '/custom-route',
            component: resolve(__dirname, 'pages/Custom.vue')
          });
        }
    }
};

````

## Updating an existing Route

Updating an existing routes can be done in two ways as listed below.

We have added new route called ``CustomRoute`` above, let's change that to some meaningful like Privacy Policy .

In first approach, we will remove the old one and add new route.

````
// nuxt.config.js

export default {
  router: {
    extendRoutes(routes, resolve) {
      // Delete automatically registered route
      routes.splice(
        routes.findIndex(route => route.path === '/custom-route'),
        1
      );

      // Re-register the same component but with different path
      routes.push({
        name: 'PrivacyPolicy',
        path: '/privacy-policy',
        component: resolve(__dirname, 'pages/Privacy.vue')
      });
    }
  }
};

````

In Second approach, we will find the required route and update the same as below:

````
// nuxt.config.js

export default {
  router: {
    extendRoutes(routes, resolve) {
      const index = routes.findIndex(route => route.path === '/custom-route');
      
      // Modify route path
      routes[index].name = 'PrivacyPolicy';
      routes[index].path = '/privacy-policy';
      routes[index].component = resolve(__dirname, 'pages/Privacy.vue');
    }
  }
};

````