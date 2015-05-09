Pa11y can be run on Cloud Foundry with few changes. This branch adds code to parse the Cloud Foundry `VCAP_APP_PORT` and `VCAP_SERVICES` environment variables for the application port and MongoDB credentials respectively. It adds [node-cfenv](https://github.com/cloudfoundry-community/node-cfenv) and [PhantomJS](http://phantomjs.org/) as `package.json` dependencies.

### Prerequisites:

1. MongoDB Brokered Service
1. [Cloud Foundry CLI](https://github.com/18F/cloud-foundry-notes/blob/master/content/getting-started/setup.md)

### Procedure:

Create a MongoDB service instance.

    cf create-service mongodb free SERVICE_NAME

Update manifest.yml placing your chosen service name in `services:` and the `MONGODB_NAME` environment variable.

	---
	applications:
	- name: pa11y
	  memory: 256M
	  services:
	    - SERVICE_NAME
	  env:
	    NODE_ENV: production
	    MONGODB_NAME: SERVICE_NAME

Launch the application.

    cf push