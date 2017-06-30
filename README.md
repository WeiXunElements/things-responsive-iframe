# things-responsive-iframe

## Responsive iFrame container for sandboxing web applications

```html
<dom-module id="admin-app-jvm">
	<template>
		<style>
			:host {
				display: block;
				@apply(--layout-vertical);
				@apply(--layout-flex);
			}
			things-code-editor {
				@apply(--layout-flex);
			}
		</style>

		<things-responsive-iframe resource-url="[[jvmMonitorUrl]]">
		</things-responsive-iframe>
	</template>
 
	<script>
		Polymer({
			is: 'admin-app-jvm',
 
			properties: {
				/**
				 * Application ID
				 */
				resourceId: {
					type: String
				},

				/**
				 * Selected application information 
				 */
				resource: {
					type: Object,
					observer: 'resourceChanged'
				},

				/**
				 * Management URL 
				 */
				managementUrl: {
					type: String
				},

				/**
				 * App Agent Port
				 */
				appAgentPort: {
					type: String
				},

				/**
				 * JVM Monitor URL 
				 */
				jvmMonitorUrl: {
					type: String,
					computed: '_computeJvmMonitorUrl(managementUrl, appAgentPort)'
				}
			},

			/**
			 * Refresh
			 */
			refresh: function() {
			},

			/**
			 * When Application selection is changed
			 *
			 * @param {Object} resource
			 */
			resourceChanged: function(resource) {
				this.resourceUrl = resource.managementUrl;
				this.resourceId = resource.id;
				var managementUrl = resource.managementUrl;
				var portSep = managementUrl.lastIndexOf(':');

				if(managementUrl.lastIndexOf(':') > 6) {
					this.managementUrl = managementUrl.substr(0, portSep);
				} else {
					this.managementUrl = managementUrl;
				}
			},

			/**
			 * Calculation of jvmMonitorUrl with managementUrl, appAgentPort
			 *
			 * @param {String} managementUrl
			 * @param {String} appAgentPort
			 */
			_computeJvmMonitorUrl: function(managementUrl, appAgentPort) {
				return managementUrl + ':' + appAgentPort + '/jvm/gauges';
			}
		})
	</script>
</dom-module>
```


## Dependencies

Element dependencies are managed via [Bower](http://bower.io/). You can install that via:

    npm install -g bower

Then, go ahead and download the element's dependencies:

    bower install


## Playing With Your Element

If you wish to work on your element in isolation, we recommend that you use
[Polyserve](https://github.com/PolymerLabs/polyserve) to keep your element's
bower dependencies in line. You can install it via:

    npm install -g polymer-cli

And you can run it via:

    polymer serve

Once running, you can preview your element at
`http://localhost:8080/components/things-responsive-iframe/`, where `things-responsive-iframe` is the name of the directory containing it.