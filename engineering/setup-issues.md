<!-- TITLE: Dev Setup Issues -->
<!-- SUBTITLE: Common gotchas and workarounds -->

See [Dev Setup](/engineering/devsetup)
# Dev Setup Issues
## Debugging localstack
Run `localstack --debug start`
### Past issues
* `Error: Unable to access jarfile /home/nate/.local/lib/python3.6/site-packages/localstack/infra/elasticmq/elasticmq-server.jar`
    * Solution: copy the jar from a teammate

## React
### The server does not recompile
Update the amount of files React can watch for changes by following [these](https://stackoverflow.com/a/60500802) instructions. (And restart your server)