# K8S Deploy Script

This project uses jinja to parse env variable into kubenetes manifest in order to use a template manifest for multiple environments

### Why not use already existing tools?

What is described next might be wrong due to lack of knowdledge of the tool or just outdated

#### Kustomize

Event though it is included in kubectl, it does not get along too well with environment variables(for some reason) and requires you to some withcraft in order to make ot work.


#### Helm

Sure, Helm works, but it requires to support a whole new tool just to apply a manifest in a cluster, which is my current use case, so yeah... seems like an overkill


#### Any other closed sourced or propietary parsing method

No... just no.


### How to use?

The script expects to receive the name of the template as an argument in the following way:

python main.py base_template.yaml

Note: as of current, the template must be in the same depth as the script

### Expected variables

#### System variables

These variables must be defined as en environment variable with the 'APP_' prefix, the templates included require the following to work as expected:

- APP_NAMESPACE: namespace where the resources will be deployed
- APP_NAME: name of the app to be included in the resources name
- APP_INGRESS_PATH: ingress path rule to be included
- APP_PR (only for merge request, pull requests): id of the reference of the pull request/merge request
- APP_TAG (only for production): id of the reference of the tag

#### Secrets

You can include secrets to your deployment and create them at once including environment variables with the prefix 'ENV_', for example creating a variable called 'ENV_DB_HOST' will create a secret containg a field called 'DB_HOST' and add it as a secret reference to your deployment with the same name.
