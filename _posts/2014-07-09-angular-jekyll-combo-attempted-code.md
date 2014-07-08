---
---

## Attempt to Generate States Using Jekyll

Listing 1.

    myApp.config(function ($stateProvider, $urlRouterProvider) {
    
        function getNameFromUrl(x) {
            return x.replace(/^[\/]+|[\/]+$/gm,'').replace('/', '-').replace(/\.[a-z]{2,4}$/, '');
        }
    
        $urlRouterProvider.otherwise('{{site.baseurl}}/recipes/chicken-curry');
    
        var routeName;
    
        //{% for p in site.pages %}
    
        routeName = getNameFromUrl('{{p.url}}').
    
        $stateProvider
        .state(routeName, {
            url: '{{ p.url }}',
            templateUrl: '{{site.baseurl}}/pages/recipes/chicken-curry.html'
        });
    
        //{% endfor %}
    }); 

This is not working.

