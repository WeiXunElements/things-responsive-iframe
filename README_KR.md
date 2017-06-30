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
				 * 애플리케이션 ID
				 */
				resourceId: {
					type: String
				},

				/**
				 * 선택된 애플리케이션 정보 
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
			 * Application 선택이 변경된 경우
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
			 * managementUrl, appAgentPort로 jvmMonitorUrl을 계산 
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

## Install the Polymer-CLI

First, make sure you have the [Polymer CLI](https://www.npmjs.com/package/polymer-cli) installed. Then run `polymer serve` to serve your application locally.

## Viewing Your Application

```
$ polymer serve
```

## Building Your Application

```
$ polymer build
```

This will create a `build/` folder with `bundled/` and `unbundled/` sub-folders
containing a bundled (Vulcanized) and unbundled builds, both run through HTML,
CSS, and JS optimizers.

You can serve the built versions by giving `polymer serve` a folder to serve
from:

```
$ polymer serve build/bundled
```

## Running Tests

```
$ polymer test
```

Your application is already set up to be tested via [web-component-tester](https://github.com/Polymer/web-component-tester). Run `polymer test` to run your application's test suite locally.
