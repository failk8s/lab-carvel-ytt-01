For the next part of this workshop we are going to use the template enabled
resource files in the ``templates-v1`` sub directory.

```terminal:execute
command: tree templates-v1/
```

Before we look at them, let's first show how the files are processed using
``ytt``. To do this run:

```terminal:execute
command: ytt -f templates-v1/
```

This is exactly the same output as the original resources we used. You can
verify this by running:

```terminal:execute
command: |-
  ytt -f templates-v1/ > /tmp/resources.yaml && \
    kapp deploy -a website -f /tmp/resources.yaml --diff-changes
```
