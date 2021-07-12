In this latest example using ``ytt`` we relied on the template versions of the
resources being filled out with default values. These default values were
defined in the ``templates-v1/values.yaml`` file.

```editor:open-file
file: ~/exercises/templates-v1/values.yaml
```

You should find:

```
#@data/values
---
website:
  name: website
```

The ``#@data/values`` comment is a special marker interpreted by ``ytt`` which
indicates that this file contains defaults for the input data values used by
these templates.

When running ``ytt`` to process the template files, there are a number of ways
you can override the default data values. The easiest to access of these is to
override a data value directly on the command line when running ``ytt``. For
example, to override the data value for the website name run:

```terminal:execute
command: ytt -f templates-v1/ -v website.name=website-1
```

You can see how instead of the names of the resources, the label values and
label selector being ``website``, it is now ``website-1``.

Create a deployment for this using:

```terminal:execute
command: ytt -f templates-v1/ -v website.name=website-1 | kapp deploy -a website-1 -f - -y
```

Then run the command again, but this time using ``website-2``, ensuring that
this application name is also supplied to ``kapp`` using the ``-a`` argument.

```terminal:execute
command: ytt -f templates-v1/ -v website.name=website-2 | kapp deploy -a website-2 -f - -y
```

List the applications ``kapp`` knows about using:

```terminal:execute
command: kapp list
```

and you should get:

```
Target cluster 'https://10.96.0.1:443'

Apps in namespace '{{session_namespace}}'

Name       Namespaces                  Lcs   Lca  
website    {{session_namespace}}  true  26m  
website-1  {{session_namespace}}  true  21s  
website-2  {{session_namespace}}  true  11s  

Lcs: Last Change Successful
Lca: Last Change Age

3 apps

Succeeded
```

We were thus able to easily create multiple instances of the application
from the same template resource files.
