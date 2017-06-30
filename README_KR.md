# things-responsive-iframe

## 이는 sandboxing 웹 애플리케이션을 위한 반응형 iFrame 컨테이너이다.

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


## Dependencies

element의 종속성은 [Bower](http://bower.io/)를 통해 관리되며, 아래의 방법을 통해 설치할 수 있다.

    npm install -g bower

다음, element의 종속성을 다운로드한다.

    bower install


## Playing With Your Element

element를 독립적으로 처리하려면 [Polyserve](https://github.com/PolymerLabs/polyserve)를 사용하여 element의 bower 의존성을 유지하도록 하며, 이는 아래의 방법을 통해 설치할 수 있다.

    npm install -g polymer-cli

그리고, 아래의 방법을 통해 실행할 수 있다.

    polymer serve

element를 실행한 경우, `things-responsive-iframe`이 디렉토리 이름으로 포함되어 있는 `http://localhost:8080/components/things-responsive-iframe/`을 통해 이를 미리 확인할 수 있다. 
