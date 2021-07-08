```terminal:execute
command: kapp deploy -a website -f resources-v1/
```

```terminal:input
text: y
```

```terminal:execute
command: kapp list
```

```terminal:execute
command: kubectl rollout status deployment/website
```

```terminal:execute
command: curl http://website.{{session_namespace}}.svc.cluster.local
```

```terminal:execute
command: kapp delete -a website -y
```
