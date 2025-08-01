# `argocd proj role remove-policy` Command Reference

## argocd proj role remove-policy

Remove a policy from a role within a project

```
argocd proj role remove-policy PROJECT ROLE-NAME [flags]
```

### Examples

```
List the policy of the test-role before removing a policy
$ argocd proj role get test-project test-role
Role Name:     test-role
Description:
Policies:
p, proj:test-project:test-role, projects, get, test-project, allow
p, proj:test-project:test-role, applications, update, test-project/project, allow
p, proj:test-project:test-role, logs, get, test-project/project, allow
JWT Tokens:
ID          ISSUED-AT                                EXPIRES-AT
1696759698  2023-10-08T11:08:18+01:00 (3 hours ago)  <none>

# Remove the policy to allow update to objects
$ argocd proj role remove-policy test-project test-role -a update -p allow -o project

# The role should be removed now.
$ argocd proj role get test-project test-role
Role Name:     test-role
Description:
Policies:
p, proj:test-project:test-role, projects, get, test-project, allow
p, proj:test-project:test-role, logs, get, test-project/project, allow
JWT Tokens:
ID          ISSUED-AT                                EXPIRES-AT
1696759698  2023-10-08T11:08:18+01:00 (4 hours ago)  <none>


# Remove the logs read policy
$ argocd proj role remove-policy test-project test-role -a get -p allow -o project -r logs

# The role should be removed now.
$ argocd proj role get test-project test-role
Role Name:     test-role
Description:
Policies:
p, proj:test-project:test-role, projects, get, test-project, allow
JWT Tokens:
ID          ISSUED-AT                                EXPIRES-AT
1696759698  2023-10-08T11:08:18+01:00 (4 hours ago)  <none>

```

### Options

```
  -a, --action string       Action to grant/deny permission on (e.g. get, create, list, update, delete)
  -h, --help                help for remove-policy
  -o, --object string       Object within the project to grant/deny access.  Use '*' for a wildcard. Will want access to '<project>/<object>'
  -p, --permission string   Whether to allow or deny access to object with the action.  This can only be 'allow' or 'deny' (default "allow")
  -r, --resource string     Resource e.g. 'applications', 'applicationsets', 'logs', 'exec', etc. (default "applications")
```

### Options inherited from parent commands

```
      --argocd-context string           The name of the Argo-CD server context to use
      --auth-token string               Authentication token; set this or the ARGOCD_AUTH_TOKEN environment variable
      --client-crt string               Client certificate file
      --client-crt-key string           Client certificate key file
      --config string                   Path to Argo CD config (default "/home/user/.config/argocd/config")
      --controller-name string          Name of the Argo CD Application controller; set this or the ARGOCD_APPLICATION_CONTROLLER_NAME environment variable when the controller's name label differs from the default, for example when installing via the Helm chart (default "argocd-application-controller")
      --core                            If set to true then CLI talks directly to Kubernetes instead of talking to Argo CD API server
      --grpc-web                        Enables gRPC-web protocol. Useful if Argo CD server is behind proxy which does not support HTTP2.
      --grpc-web-root-path string       Enables gRPC-web protocol. Useful if Argo CD server is behind proxy which does not support HTTP2. Set web root.
  -H, --header strings                  Sets additional header to all requests made by Argo CD CLI. (Can be repeated multiple times to add multiple headers, also supports comma separated headers)
      --http-retry-max int              Maximum number of retries to establish http connection to Argo CD server
      --insecure                        Skip server certificate and domain verification
      --kube-context string             Directs the command to the given kube-context
      --logformat string                Set the logging format. One of: json|text (default "json")
      --loglevel string                 Set the logging level. One of: debug|info|warn|error (default "info")
      --plaintext                       Disable TLS
      --port-forward                    Connect to a random argocd-server port using port forwarding
      --port-forward-namespace string   Namespace name which should be used for port forwarding
      --prompts-enabled                 Force optional interactive prompts to be enabled or disabled, overriding local configuration. If not specified, the local configuration value will be used, which is false by default.
      --redis-compress string           Enable this if the application controller is configured with redis compression enabled. (possible values: gzip, none) (default "gzip")
      --redis-haproxy-name string       Name of the Redis HA Proxy; set this or the ARGOCD_REDIS_HAPROXY_NAME environment variable when the HA Proxy's name label differs from the default, for example when installing via the Helm chart (default "argocd-redis-ha-haproxy")
      --redis-name string               Name of the Redis deployment; set this or the ARGOCD_REDIS_NAME environment variable when the Redis's name label differs from the default, for example when installing via the Helm chart (default "argocd-redis")
      --repo-server-name string         Name of the Argo CD Repo server; set this or the ARGOCD_REPO_SERVER_NAME environment variable when the server's name label differs from the default, for example when installing via the Helm chart (default "argocd-repo-server")
      --server string                   Argo CD server address
      --server-crt string               Server certificate file
      --server-name string              Name of the Argo CD API server; set this or the ARGOCD_SERVER_NAME environment variable when the server's name label differs from the default, for example when installing via the Helm chart (default "argocd-server")
```

### SEE ALSO

* [argocd proj role](argocd_proj_role.md)	 - Manage a project's roles

