vuetable - data table simplify!
========

- No need to render the table yourself
- One simple `vuetable` tag
- Display data retrieved from server with sort options
- Pagination component included, swap-able and extensible
- Define fields to map your JSON data structure
- Define row actions and capture the click event to do whatever you want
- Field display customizable via callback function inside Vue.js instance
- Programmatically show/hide any field via reactivity of fields definition
- Use your favorite CSS framework classes to nicely format your table and dispalyed data
- Events to allow control from Vue.js instance programmatically
- Capture events from `vuetable` to manipulate your table and your data
- Should work with any pre-defined JSON data structure
- Should work with any CSS Framework, e.g. Semantic UI, Twitter's Bootstrap

---

##Live Demo
- [JSON data structure](http://vuetable.ratiw.net/api/users)
- [Semantic UI example](http://vuetable.ratiw.net/examples/semantic.html)
- [Bootstrap UI example](http://vuetable.ratiw.net/examples/bootstrap.html)

---

## What is `vuetable`?
`vuetable` is a Vue.js component that will automatically request (JSON) data
from the server and display them nicely in html table with swappable/extensible
pagination sub-component. You can also add buttons to each row and hook an event
to it

![image](https://i.imgsafe.org/d46e5e1.gif)

> Please note that all the examples show in here are styling using Semantic UI CSS Framework,
> but `vuetable` should be able to work with any CSS framwork including Twitter's Bootstrap.
> Please read through and see more info [below](#bootstrap).

You do this:
```html
    <div id="app" class="ui vertical stripe segment">
        <div class="ui container">
            <div id="content" class="ui basic segment">
                <h3 class="ui header">List of Users</h3>
                <vuetable
                    api-url="http://example.app:8000/api/users"
                    table-wrapper="#content"
                    :fields="columns"
                    :item-actions="itemActions"
                ></vuetable>
            </div>
        </div>
    </div>
```

```javascript
	<script>
	    new Vue({
	        el: '#app',
	        data: {
	            columns: [
	                'name',
	                'nickname',
	                'email',
	                'birthdate',
	                'gender',
	                '__actions'
				],
	            itemActions: [
	                { name: 'view-item', label: '', icon: 'zoom icon', class: 'ui teal button' },
	                { name: 'edit-item', label: '', icon: 'edit icon', class: 'ui orange button'},
	                { name: 'delete-item', label: '', icon: 'delete icon', class: 'ui red button' }
	            ]
	        },
	        methods: {
	            viewProfile: function(id) {
	                console.log('view profile with id:', id)
	            }
	        },
	        events: {
	            'vuetable:action': function(action, data) {
	                console.log('vuetable:action', action, data)
	                if (action == 'view-item') {
	                    this.viewProfile(data.id)
	                }
	            },
	            'vuetable:load-error': function(response) {
	                console.log('Load Error: ', response)
	            }
	        }
        })
	</script>
```

And you get this!
![image](https://i.imgsafe.org/af08442.jpg)

Since I'm mainly using [Semantic UI](http://semantic-ui.com) as my default CSS Framework, all the css
styles in `vuetable` are based on Semantic UI. If you're using Twitter's [Bootstrap](http://getbootstrap.com)
css framework, please see [documentation in the Wiki pages](https://github.com/ratiw/vue-table/wiki/Using-%60vuetable%60-with-Twitter's-Bootstrap).

## Usage

### Bower

```
$ bower install vuetable
```

### NPM

```
$ npm install vuetable
```

### Direct include

Just import the `vue-table.js` after `vue.js` and `vue-resource.js` library in your page like so.
```html
	<script src="js/vue.js"></script>
	<script src="js/vue-resource.js"></script>
	<script src="js/vue-table.js"></script>
```

Then, reference the vuetable via `<vuetable>` tag as following

```html
	<div id="app">
	    <vuetable
	        api-url="/api/users"
	        :fields="columns"
	    ></vuetable>
    </div>

	<script>
		new Vue({
			el: '#app',
			columns: [
				'firstname',
				'lastname',
				'nickname',
				'birthdate',
				'group.name_en'
				'gender',
				'last_login',
				'__actions'
			]
		})
	</script>
```
- `api-url` is the url of the api that `vuetable` should request data from.
The returned data must be in the form of JSON formatted with at least the number of fields
defined in `fields` property.
- `fields` is the fields mapping that will be used to display data in the table.
You can provide only the name of the fields to be used. But if you would like to get
the true power of `vuetable`, you must provide some more information.
Please see [Field Definition](https://github.com/ratiw/vue-table/wiki/Fields-Definition)
section for more detail.

For more detail, please see [documentation in the Wiki pages](https://github.com/ratiw/vue-table/wiki).


<a id="license"></a>
## License
`vuetable` is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).
