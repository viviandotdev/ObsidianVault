---
modified: 2025-07-18T07:58:17-04:00
---
```
{% if is_new_article %}
tags::
{% if link %}source:: {{link}}{% endif %}
type:: #source/{{type}}

### {{title}}

{% if excerpt %}{{excerpt}}{% endif %}

#### Highlights
{% endif -%}{% for highlight in highlights %}
{% if highlight.color == "red" -%}
    {%- set callout = "danger" -%}
{%- elif highlight.color == "blue" -%}
    {%- set callout = "info" -%}
{%- elif highlight.color == "green" -%}
    {%- set callout = "check" -%}
{%- else -%}
    {%- set callout = "quote" -%}
{%- endif -%}
> [!{{callout}}]+ Updated on {{highlight.lastUpdate}}
>
> {{highlight.text.split("\n") | join("\n>")}}
{% if highlight.note -%}> > {{highlight.note + "\n"}}{%- endif %}

{%- endfor -%}

```