---
---

## Generate The Add State Code for Each Page and Post Using Jekyll

{% raw %}

    var pageUrls = [];

    // {% for p in site.pages %}{% if p.url contains '.html' %}{% unless p.url contains 'index.html' %}
    pageUrls.push('{{ p.url }}');// {% endunless %}{% endif %}{% endfor %}

    // {% for p in site.posts %}
    pageUrls.push('{{ p.url }}');//{% endfor %}

    for (i = 0; i < pageUrls.length; i++){
        $stateProvider.state(getNameFromUrl(pageUrls[i]), {
            url: pageUrls[i].replace(/\.[a-z]{2,4}$/, ''),
            templateUrl: '{{ site.baseurl }}' + pageUrls[i]
        });
    }

{% endraw %}

### Using 'if' to effectively achieve a 'where' clause.

{% raw %}

    {% for collection in product.collections %}
      {% if collection.title == 'Sale' %}
        {% assign in_sale_collection = true %}
      {% endif %}
    {% endfor %}
    
{% endraw %}


### Can't use html5 mode without some server configuration

Can't use html5 mode because a user may navigate directly to a route
at which point Angular is not loaded and the server will send back
a 404 error. This could be resolved with some simple server configuration
but here we are creating ultra simple application that can run anywhere.
        
    myApp.config(["$locationProvider", function($locationProvider) {
        $locationProvider.html5Mode(true);
    }]);
    
### Jekyll Post and Page Properties

Posts are treated differently to pages. Jekyll infers quite a bit of information
from the file name of a post. If not provided in the front matter, Jekyll will
assign a value for `title` and `id`. If not in the yaml front matter these properties
will not exist for pages.

### Configuring the PermaLinks

Adding `permalink: /:year/:month/:title/` to the _config.yml file causes Jekyll
to create a folder for each post within which there will be an index.html file.
E.g. 2014/07/09/some-post/index.html. This enables pretty URLs (without the 
file extension, but that makes no difference if we are not accessing the files
directly but instead using them as AngularJs templates.

If we have `permalink: /:year/:month/:title` (without the final /) we will get 
html files without the last folder. E.g. 2014/07/09/some-post.html. This is the 
default - what you get if you omit the permalink property.

`permalink: /:year:month:day-:title` will produce URLs 20140709-some-post.html.



### There May be No Difference Between Pages and Posts in Angular-Jekyll App

Given we are not using the pretty routes feature of Posts (where Jekyll creates
the required folders and files according to permalink settings) there may be no
difference between a post and a page.

### Returning A Single Promise from a Service

    resolve: {
        r: function(dataservice){
            return dataservice.getReferences();
        }
    }
    
And dataservice looks like this:

    myApp.factory('dataservice', ['$http', function($http) {

        return{
            getReferences: function(){
                return $http.get('http://localhost:8000/sandpit/ngData/references.yml');
            }
        }
    }]);
    
But we want to change it so it only hits the server once.

