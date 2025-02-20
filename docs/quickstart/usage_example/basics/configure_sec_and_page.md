---
title: Configure your section and page
cover: assets/logo.svg
---

This demo shows you how to configure your demo page and sections.

By default, a demo section takes the folder name as its section title, and it
takes the file orders as its card orders, which can be unsatisfying in many cases.
Luckily, `DemoCards.jl` reads the `config.json` file in the section folder, for example:

```json
{
    "title": "Basic Usage",
    "order": [
        "simple_markdown_demo.md",
        "configure_with_yaml.md"
    ]
}
```

A demo page is maintained in a similar manner, except that it needs extra keys to configure the template
page. For example:

```json
{
    "template": "template.md",
    "theme": "grid",
    "order": [
        "basic",
        "advanced"
    ]
}
```

If `template` is not specified, `"index.md"` will be used if available, otherwise, it will use a
blank template generated by DemoCards.

There are three possible options for `theme`:

* `"nothing"`: It won't generate the index page, instead, it will use the sidebar generated by
  Documenter for navigation purpose. `template` option doesn't affect, neither.
* `"grid"`: a grid like index page.
* `"list"`: a list like index page.

You can check the "Theme Gallery" to see how different themes look like.


## [Override default values with properties](@ref page_sec_properties)

Another item that could be useful is `properties`, it is written as a dictionary-like format, and
provides a way to override some default values. Properties can be configured at any level and it
follows very simple rules:

- Properties at a higher level item can be propagated into lower level items
- Properties at lower level items are of higher priority


```text
example_page/
├── config.json
├── sec1
│   ├── config.json
│   ├── demo1.jl
│   ├── demo2.jl
│   └── demo3.md
└── sec2
    ├── demo4.jl
    └── demo5.jl
```

For example, in the above folder structure, if we configure `example_page/config.json` with

```json
{
    "properties":{
        "notebook": "false"
    }
}
```

Then all julia demos will not generate jupyter notebook unless it's override somewhere in the lower
level, e.g, `sec1/config.json` or `demo1.jl`.


Only a subset of demo entries support the property propagation, currently supported items are:

* Julia files: `notebook` allows you to enable/disable the jupyter notebook generation.
