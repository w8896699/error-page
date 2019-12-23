# ErrorPage

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 8.3.17.

## Development server

Run `ng start` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.


## For OpenShift Deployment

Deploment Config and Build Config are been placed in openshift directory as dc.yaml and bc.yaml

### Usage

We have to process and build the application before we deploy it. 

#### bc.yaml Usage:

bc.yaml will need couple parameters: A name used for all objects, A version used for the image tags, node.js version ,source respository url and Source repository branch, we can put all those parameter in one file and process them together, here's a example I made for parameter.sh:
```
NAME=err-page
VERSION=v1.0.0
NODE_JS_VERSION=10
SOURCE_REPOSITORY_URL=https://github.com/w8896699/error-page
SOURCE_REPOSITORY_REF=master
```
Then we need to process the bc.yaml with these parameter:
```
oc process -f bc.yaml --param-file parameter.sh | oc apply -f -
```

#### dc.yaml Usage:
After build process is finished, We need dc.yaml to deploy this application into some namespace
here's how we can use it, again, some parameters: A version used for the image tags, A name used for all objects

```
oc process -f dc.yaml -n <namespace> -p NAME=err-page VERSION=v1.0.0  | oc apply -f -
```