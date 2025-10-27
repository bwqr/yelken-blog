+++
title = "Yelken's Last Alpha Release and Intro to Yelken Cloud"
date = 2025-10-28
+++

Hi everyone!

Welcome to the third and, hopefully, last planned alpha release of Yelken where the next release should be a beta one.
To quickly describe Yelken, it is a Next-Generation Content Management System (CMS) with the goal of being Secure by Design, Extendable, and Speedy.
It is free for everyone to use, and its source code is available on [GitHub](https://github.com/bwqr/yelken).
If you want to learn more about Yelken, I highly encourage you to read the [first announcement](/first-announcement/) post.

It's been a long time since the [second alpha release announcement](/second-alpha-release), precisely 5 months!
During this period, Yelken underwent heavy development to implement its basic features and define its architecture.
At this point, I believe Yelken has reached a state where users can manage their website from the App (an admin dashboard for users), albeit in a primitive way.

In addition to Yelken developments, Yelken Cloud, which is a complementary project to Yelken, is also ready with its first alpha release.
It has gained the necessary features to provide a SaaS experience for Yelken.
To let you experiment with the Yelken Cloud and provide feedback without any cost, an **Open Alpha** testing period is being carried out that will end on **15 November 2025**.
You can visit [cloud.yelken.io](https://cloud.yelken.io) to sign up and test both Yelken and Yelken Cloud for free and share your experience with us in the [Support](https://cloud.yelken.io/support/tickets) section or through other communication channels.
Please be aware that this is an **Open Alpha**, and do not expect any changes you make to persist indefinitely.

If you want to have a quick experience with Yelken without getting into the details, you can try [Playground](https://playground.yelken.io), which creates a new Yelken instance running entirely in your browser.
Otherwise, let's proceed with the details about the latest developments.

### Yelken

With the third alpha release, Yelken now features a functional App where users can manage their content, customize the appearance of the site, and perform administrative operations.
Let's have a glance at the App:

![Yelken CMS Alpha3 App](/yelken-alpha3.png)

As shown in the image above, Yelken currently has three different areas of interest: CMS, Appearance, and Administration.
In the CMS section, you can create new models that define the structure of your content.
Later, you can create contents for a specific model.
Additionally, you can upload new assets, such as media files, into the system to be used inside your content.

While the CMS section enables you to define your content, the Appearance section allows you to determine how it is displayed on your website.
You can install new themes to change the appearance of your website easily, or you can also create custom templates to render them in specific pages.

Yelken also enables you to create new users to let teams manage a Yelken website collaboratively. Permissions of each user can be adjusted according to your team's needs.
You can also create roles with a set of permissions and assign users to roles.

To learn more about using the Yelken, please refer to the documentation located in the [Yelken Book](https://docs.yelken.io).
Also, note that the book has some missing sections as well as some under-documented sections.
We are trying to improve the documentation with each passing day.
You can open issues about possible improvements in the book's [GitHub repository](https://github.com/bwqr/yelken-book).

### Yelken Cloud

Next to Yelken, we are also developing Yelken Cloud, which enables you to create a fresh website powered by Yelken with a few clicks.
It provides a managed Yelken experience where Yelken Cloud handles the infrastructure and maintenance.
With this announcement, we are providing an Open Alpha testing period, allowing you to experiment with the Yelken Cloud at no cost and provide feedback until **15 November 2025**.
You can join us during this period and help improve both Yelken and Cloud service by sharing your experience.
Check the [Cloud page](https://yelken.io/cloud) for more information.

Inside the Yelken Cloud, you can create a new website by creating a new Project.
You can also use your custom domain to access your website.
However, HTTPS access over a custom domain is not currently implemented.
You also need to create a DNS record that points your domain to our servers; however, the type of DNS record and its value have not been finalized yet.

As another feature, you can invite other users to your team to allow them access to your websites and manage them.
There is also a *Billing* page in the Yelken Cloud.
You can track the cost of your projects, which is obviously free in this Open Alpha.

### Next Step

According to the [Yelken 0.1.0 Project](https://github.com/users/bwqr/projects/3), we have a few features remaining that have not been implemented, namely Form, Observability, and Plugin features.
Besides these, Yelken's current architecture has a few open design issues that need to be solved for future development.
However, before starting work on these items, we would like to receive extensive feedback about the current state of Yelken from you, whether it is about documentation or anything else.
For this reason, we are open answering any questions you may have.

### Contributing

As described in the [Next Step](#next-step) section, the best way to contribute to Yelken at the moment is by testing and providing feedback on its current state.
Yelken needs your feedback to shape its future.
Share your experience with us through communication channels.

## Learn more
Here are a few links to check out more about Yelken:

* Website [yelken.io](https://yelken.io)
* Repository: [github.com/bwqr/yelken](https://github.com/bwqr/yelken)
* Book: [docs.yelken.io](https://bwqr.github.io/yelken-book)
* Blog: [blog.yelken.io](https://blog.yelken.io)
* Playground: [playground.yelken.io](https://playground.yelken.io)
* Examples: [github.com/bwqr/yelken/tree/main/examples](https://github.com/bwqr/yelken/tree/main/examples)
* Discord server: [discord.gg/D4bfHr8neh](https://discord.gg/D4bfHr8neh)
