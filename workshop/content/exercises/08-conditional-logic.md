```terminal:execute
command: ytt -f templates-v2 -v website.name=website-3 -v website.ingress.hostname={{session_namespace}}-website -v website.ingress.domain={{ingress_domain}}
```
