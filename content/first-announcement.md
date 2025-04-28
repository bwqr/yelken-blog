+++
title = "Yelken Alpha Release Announcement"
date = 2025-05-01
+++

Welcome to Yelken's first alpha release announcement, a project described as a *Secure by Design, Extendable, and Speedy Next-Generation Content Management System (CMS)*.
Yelken is a traditional CMS where you can both manage your contents (backend) and present them to your users (frontend).

Literary, Yelken is a Turkish noun that means **sail** in English (check out [TDK](https://sozluk.gov.tr/?ara=yelken) for its pronunciation).
It is free for everyone to use, and its source code is available on [GitHub](https://github.com/bwqr/yelken).
Under the hood, Yelken utilizes [Rust](https://www.rust-lang.org/) programming language and libraries developed around it to achieve its goals.
The project is still under heavy development and may contain bugs or missing some features, but it is ready to be tested and experimented with this first alpha release.
You can check out the [examples](https://github.com/bwqr/yelken/tree/main/examples) folder in the repository to see Yelken in action.

While many CMS projects exist, such as traditional ones like WordPress and Drupal or headless ones, Yelken has many ambitious goals to distinguish itself from others.
This distinction is observable in its description, where each word has a strong meaning in the Yelken and defines its identity.

To begin with *Secure by Design*, Yelken's highest priority is keeping itself from being infected by malicious user input or a malicious plugin.
No matter what input is given to Yelken, it must continue sustaining its functionalities and not unintentionally affect other users, such as causing cross-site scripting (XSS) and other possible attacks.
A plugin also must not alter the behavior of the system permanently.
If a plugin causes any undesired effect on the system, admins must be able to disable it and make the system return to its original behavior.

Another essential aspect of Yelken is its *Extendable* architecture with plugins.
Yelken utilizes [WebAssembly System Interface (WASI) Preview 2](https://github.com/WebAssembly/WASI/blob/main/wasip2/README.md) and defines a set of interfaces for plugins to interact with Yelken.
WebAssembly enables developers to use their favorite programming languages that support WebAssembly, such as low-level languages C, C++, and Rust, or high-level languages Javascript and Python, and develop plugins for Yelken.
The diversity of supported programming languages should bring developers with different backgrounds into Yelken plugin development.
The capabilities of plugins are still under investigation, but the plugin architecture has been solidified in Yelken.

Lastly, besides security and extendability, Yelken aims to be a *Speedy* CMS by requiring very low computing resources (CPU and memory mainly) and serving many requests concurrently and quickly.
Thanks to the software stack Yelken uses, hosting many Yelken instances on a computing device with very few resources is easy.

In addition to ambitious goals, Yelken tries to be user-friendly from out of the box with sane defaults and easy to deploy to any hosting solutions.
However, it also gives you enough power to customize it according to your liking or revert to its original behavior thanks to its layered approach.

After talking about the goals of Yelken, we can now discuss its features expected from a CMS.

## Features
Aside from three main goals, Yelken has many features built into itself to provide a greater out-of-the-box experience and reduce the number of required plugins installed.
These features are an advanced permission system, built-in localization (l10n) support, themes and a powerful templating system, structured content management, and dynamic pages to decide what to render at which URL path.

These are not all the features Yelken has implemented.
There are also features, such as form handling, observability, and asset management, that are planned to be added to Yelken in the near future.

### Localization
L10n support in Yelken sits at its core and is strongly related to other features.
A Yelken instance can have one or more locales defined to provide localized URL paths, texts in templates, and contents.

To enable themes to translate static texts found in their templates, Yelken uses [Fluent](https://projectfluent.org/) localization system.
Themes can provide default translations for the static texts in their templates by providing necessary fluent files.
Users can also override these translations either globally or scoped per theme.

URL paths of displayed pages can also be localized.
For instance, you might have a page at `/article/{id}` displaying an article identified with `id` path parameter in English.
You can also have a corresponding Turkish page at path `/makale/{id}` displaying the same article in Turkish.
Behind the scenes, these two pages are linked with the same `name`, enabling localizing the link inside the HTML anchor tag.
```html
<a href="{{ localize_url(page='article', params=[article.id]) }}">
  {{ article.title }}
</a>
```

Finally, to enable content localization, each field of a model can be marked as localizable, allowing admins to create different values for each locale while creating or updating a content's field.
If a field is not marked as localizable, its single value can be used regardless of the resolved locale.

### Theme & Template
Yelken enables users to customize the look of their website by installing a theme.
There can be many different themes installed on the Yelken, but only one can be active at a time.
A theme consists of templates, contents, and pages to render an HTML document for a given URL path.

Speaking of templates, Yelken uses a template engine based on [Jinja2](https://jinja.palletsprojects.com/en/stable/) to render a page and display it to users.
Inside templates, Yelken exposes various variables and functions to let theme developers or users access information about request, such as locale and path params, and load contents to display them.

In terms of customizing a theme, users can easily customize the active theme by modifying parts of its templates.
As was the case for overriding the translations, templates can be overridden either globally or scoped per theme.

### Content Management
Yelken's Content management is anticipated to be the most frequently used feature of the project.
It also hosts many sub-features to make using the Yelken a breeze. In the Content feature, multiple components help manage content easily:

* Models

  They define the shape of content. Models are composed of many individual fields to form a shape.

* Fields

  They define the type of input that will be received from the admin during content creation.
  The most basic field is text, which can be used to receive any kind of value from the admin.
  A special type of field is enums, where possible values are already specified.
  A field can have its own validation or parsing rules (e.g., a path field can store its values syntactically as a string while it semantically means a URL segment and can contain only valid URL segments).
  Many different fields can be built into Yelken or provided by the admin or plugins.

* Contents

  Once admins set up their desired models and fields, they can start creating content for a given model by providing values for each field of the model.

To ease the management of content, there are a few content-specific features:

* Stages

  A content can be in one of the stages to differentiate between draft and published ones.
  As it can be guessed, published and draft can be provided as default stages. Admins may add custom stages as well.

* Scheduling

  A content can be scheduled to transition from one stage to another one. This enables publishing a content at a specified time without manually publishing it.

* Default fields

  Contents must have a set of fields by default, such as their publisher, first creation time, latest update time, stage transition time, etc.

### Page
A page comprises a URL path and template to define which template will be rendered when a user requests a URL path.
For example, we can define a page with `/article/{id}` as its URL path and `article.html` as its template.
When the user requests `/article/hello-world` URL path, Yelken will find the `article.html` template and render it.

## Current Status
In this first alpha release, most of the features above are implemented in Yelken.
However, a huge piece is missing from the puzzle.
Yelken lacks a User Interface (UI) or an admin panel.
This admin panel's infrastructure does exist, but the necessary pages and components to interact with features have not been implemented yet.
At the moment, the only possible way to interact with Yelken is by using its REST API.

Since features are still in heavy development, developing a UI and adapting it to changes does not make sense.
Once features are stabilized, I can start developing the admin panel.

## Future of Yelken
Yelken has many compelling features, most of which have been implemented.
The next step will be to implement the remaining parts, stabilize features, and fine-tune them according to the users' needs.
During this phase, there will be a couple more alpha releases, which will eventually lead to a beta release.
You can track the development from the [Yelken 0.1.0](https://github.com/users/bwqr/projects/3) project.

Afterward, the planned features can start being added to Yelken. In this case, form handling is a high priority since admins need to receive input from their users.
Secondly, a Yelken instance needs to be observable and provide metrics to inform website traffic and performance.
For this purpose, Yelken plans to expose many different metrics and display them in the admin panel.

### Plugins
The plugin feature is vital for Yelken in terms of enabling its extendability.
How plugins should be written, distributed, and installed into Yelken is settled down; however, what capabilities they need is still under investigation.
As an example, should plugins hook into the flow of a request, such as middlewares, or should they be only callable from templates by themes or users?
As a third option, a plugin can do both :).

In addition to capabilities, the plugins need a permission system that explicitly specifies what they can do to inform the admin about their possible effect on the Yelken.
This will also let us configure WebAssembly runtime to enable only required WASI parts, such as networking and filesystem access.

### SaaS Product
As a way to sustain the development of Yelken and create a revenue source, the ultimate goal is to provide Yelken as a Software as a Service (SaaS) product to people.
In this way, anyone can easily use Yelken for their website without thinking about the underlying infrastructure.
SaaS will automatically create the necessary resources for Yelken to function and hide the management part from its users.
This includes managing databases, collecting metrics from Yelken instances, enabling seamless user login, etc.

At the moment, I am not planning to add any feature that will be feature-gated behind a paid version, such as an enterprise version.
All the features you can get in the SaaS version will be available to you, too. You only need to manage all the required resources by yourself.
For example, if you need to utilize the observability feature of Yelken, you may need to set up a time series database to collect metrics periodically.

To keep this product as a revenue source for Yelken, Yelken employs a license that only restricts its usage when another company wants to provide Yelken as a SaaS product.
The following section talks about this license.

## License
Yelken is currently licensed with Business Source License 1.1.
This license is not meant to prevent any **individual** from benefitting Yelken.
Individuals can use and deploy Yelken to production.
Individuals can also use Yelken to provide paid support to setup and manage Yelken for their customers.
Even companies can utilize Yelken to manage their websites.
The primary motivation behind choosing this license is to prevent a company from providing Yelken as a SaaS product without acquiring an explicit license.

Yelken is not the first project utilizing this license and will not be the last one.
For example, you can check out [surrealdb licensing](https://github.com/surrealdb/license).
If you have any concerns about the license, you can open an Issue or Discussion on the Yelken repository or even join the Discord server, and we can discuss.

## Learn more
If this announcement makes you excited about Yelken or you want to have a more detailed view of Yelken, you can start reading [Yelken's book](https://bwqr.github.io/yelken-book/).
Additionally, here are a few links to check out more about Yelken:

* Repository: [https://github.com/bwqr/yelken](https://github.com/bwqr/yelken)
* Book: [https://bwqr.github.io/yelken-book](https://bwqr.github.io/yelken-book)
* Blog: [https://bwqr.github.io/yelken-blog](https://bwqr.github.io/yelken-blog)
* Examples: [https://github.com/bwqr/yelken/tree/main/examples](https://github.com/bwqr/yelken/tree/main/examples)
* Towards Yelken 0.1.0: [https://github.com/users/bwqr/projects/3](https://github.com/users/bwqr/projects/3)
* Discord server: [https://discord.gg/D4bfHr8neh](https://discord.gg/D4bfHr8neh)
