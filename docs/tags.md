# Variable tags

Used to print a variable to the template. If the variable is not in the context we don't get an error, rather an empty string. You can use dot notation to access object proerties or array memebers.

    <p>First Name: {{users.0.first_name}}</p>

# Comment tags

Comment tags are simply ignored. Comments can't span multitple lines.

    {# This is a comment #}

# Logic tags

## extends / block

Check django's template inheritance system for more info. Unlike django, the block tags are terminated with {% end %}, not with {% endblock %}

## include

Includes a template in it's place. The template is rendered within the current context. Does not requre closing with {% end %}.

    {% include template_path %}
    {% include "path/to/template.js" %}

## for

You can iterate arrays and objects. Access the current iteration index through 'forloop.index' which is available inside the loop.

    {% for x in y %}
      <p>{% forloop.index %}</p>
    {% end %}

## if

Supports the following expressions. No else tag yet.

    {% if x %}{% end %}
    {% if !x %}{% end %}
    {% if x operator y %}
      Operators: ==, !=, <, <=, >, >=, ===, !==, in
      The 'in' operator checks for presence in arrays too.
    {% end %}
    {% if x == 'five' %}
      The operands can be also be string or number literals
    {% end %}

## autoescape

The `autoescape` tag accepts one of two controls: `on` or `off` (default is `on` if not provided). These either turn variable auto-escaping on or off for the contents of the filter, regardless of the global setting.

For the following contexts, assume:

    some_html_output = '<p>Hello "you" & \'them\'</p>';

So the following:

    {% autoescape off %}
        {{ some_html_output }}
    {% end %}

    {% autoescape on %}
        {{ some_html_output }}
    {% end %}

Will output:

    <p>Hello "you" & 'them'</p>

    &lt;p&gt;Hello &quot;you&quot; &amp; &#39;them&#39; &lt;/p&gt;