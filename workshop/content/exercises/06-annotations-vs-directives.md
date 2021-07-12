We have seen how to process a set of templates using ``ytt`` and one way of
how we can provide data input values for our template. Now let's look at the
template files themselves and how the data values are inserted into the
resource definition.

Open up the ``templates-v1/deployment.yaml`` template file.

```editor:select-matching-text
file: ~/exercises/templates-v1/deployment.yaml
text: "name: (.*)"
isRegex: true
```

Focusing on the name property of the resource we find:

```
name: #@ data.values.website.name
```

The file format here is YAML, but against the ``name`` property we do not
actually have a value but instead have a comment.

All ``ytt`` templates are valid YAML files but details about variable
sustitutions and everything else you can place in the template is handled
through embedding comments in the YAML file.

All comments which pertain to ``ytt`` template processing start with the
``#@`` prefix but there are a couple of subtly different variants of this.

If you remember from the previous section the data values file included a line
of the form:

```
#@data/values
```

This prior example is called an annotation. This is different to what you see
in the example above for the template file, which instead is referred to as a
directive.

How do you tell the difference?

The difference is that in annotations there is no space after the comment
prefix ``#@``, where as in the case of a directive, there is at least one
space after ``#@``.

If you get these mixed up then you will get errors.
