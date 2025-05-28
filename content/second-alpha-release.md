+++
title = "Yelken Second Alpha Release"
date = 2025-05-28
+++

Welcome to Yelken's second alpha release post.
In this post, an overview of changes made to the project since its first alpha release will be presented.
Before diving into details, let us remember what the Yelken was.
Yelken describes itself as a *Secure by Design, Extendable, and Speedy Next-Generation Content Management System (CMS)*.
It is a traditional CMS where you can both manage your contents (backend) and present them to your users (frontend).
Yelken's source code is available on [GitHub](https://github.com/bwqr/yelken) and you can freely use Yelken.
You can check the [first announcement](/first-announcement/) post for a more detailed overview of Yelken.

## Progress Report

Exactly one month has passed from the first alpha release, and there are a few exciting additions to the Yelken.
First of all, there are Rest API additions related to content management.
Secondly, existing but not very usable Yelken App (formerly known as admin panel) is migrated from [Leptos](https://leptos.dev/) to [SolidJS](https://www.solidjs.com/) because of some challenges I encountered.
I am planning to write another blog post discussing them.
Aside from that, Yelken now has a [playground](https://yelken-cms.netlify.app) where you can run Yelken entirely in your browser and play with it.
This is the most important addition we have in this release.
Lastly, the foundations of Yelken Cloud (previously mentioned as Yelken SaaS) have been settled.

### Implementing missing features
While Yelken defines a set of features to provide a good CMS experience, some have not yet been implemented.
One of them is managing the models and their contents (an essential one for a CMS).
With this release, models and their contents can be created or updated via API endpoints as well as in the Yelken App.
Besides that, the **stages** feature is introduced to contents that can be in one of the defined stages.
Currently, *draft* and *published* stages are defined by default.
When content is moved to the *published* stage, it will be publicly visible to site visitors.
In the future, users can define their own stages further to differentiate the contents, such as *needs review* stage.

### Changes in Yelken App
In the first announcement post, there was a mention of the lack of a usable admin panel where users can manage their websites.
While there was a basic implementation of this panel, called Yelken App, it only provided authorization feature for users, such as login.

Originally, the Yelken App was implemented with the Leptos framework, a modern Rust web framework.
The primary motivation behind choosing Leptos was to have a framework capable of Server Side Rendering (SSR) and Client Side Rendering (CSR).
In addition, it needs to be embedded into Yelken itself to have only one single process running on a server, which will provide both Yelken and its App.
Since Yelken is written in Rust, choosing a Rust web framework was a reasonable option.
I only used Leptos's rendering capabilities and successfully integrated it into Yelken.

I parted the Yelken project into a workspace with multiple crates to have the App run both in CSR mode and SSR mode, where SSR mode was running inside the Yelken.
While developing the App, I was using CSR mode to just compile the App itself without compiling the whole Yelken to improve the iteration speed.
However, my productivity was reduced due to the challenges I encountered during the development.
To mention just two of them, compile times are not comparable to JavaScript solutions (in my case, they were between 5-10 seconds for an edit-compile iteration).
Rust-analyzer was also having some problem to provide quick actions or suggestions.
I hope to write a detailed blog post about them and discuss possible solutions.

At some point, I reevaluated the App's requirements and decided that having SSR capability is something not needed by an admin panel.
Users can wait a few more seconds for the page to load and start interacting with the App.

Following this decision, I started implementing Yelken with the SolidJS framework, which went well.
I am only using the CSR mode of SolidJS and just let it render the page.
The current implementation of the App has a strong base from which we can build a great admin panel.
The UI design is not something I am proud of, but it will be improved in the coming releases.

### Yelken Playground
I always thought of having a playground to enable people to experiment easily with the Yelken.
While we can talk about Yelken and its features, for anyone to see the Yelken in action, they need to have a running Yelken instance somewhere, such as locally or on a server.
On the other hand, having a Yelken playground where a new instance starts running freshly can definitely alleviate this requirement and allow Yelken to reach more people.

Similar to [Wordpress Playground](https://wordpress.org/playground/), this feature would enable Yelken to run entirely in the browser.
Even though my initial plan was to implement this feature in the far future, wanting others to have the experience and track the changes led me to implement this feature much sooner.
And with this release, I proudly announce that Yelken can run entirely in the browser.

The playground feature required a considerable amount of effort (roughly one week of time spent on this [PR](https://github.com/bwqr/yelken/pull/18)) to have Yelken running in the browser.
This includes changing assumptions made by Yelken about its environment and sending one or two patches to a few dependencies used by Yelken ([diesel](https://github.com/diesel-rs/diesel/pull/4616/files) and [diesel-async](https://github.com/weiznich/diesel_async/pull/236)).
With these changes, Yelken got closer to its **Make it easy to run anywhere** goal.

Under the hood, Yelken is compiled to WebAssembly while embedding some helpful files into the binary.
It also utilizes SQLite as a database instead of preferred PostgreSQL.
When the playground website is loaded by the browser, a [Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) is registered.
Within the Service Worker context, the WebAssembly binary is instantiated, and all the requests sent by the browser to any of Yelken's endpoints are directed to this running instance.

You can check [Yelken Playground](https://yelken-cms.netlify.app) to discover its capabilities.
In the playground, the controls are positioned at the top. You can use the controls to go to some specific page.
The admin user's email and password are also written at the top. You can use these credentials to log into the App by clicking **Dashboard** button.
Before closing the words on the playground feature, I want to clearly state that this playground shows how immature Yelken currently is.

### Yelken Cloud
As discussed in the first announcement post, the ultimate goal is to provide Yelken as a Software as a Service (SaaS) product.
For this purpose, a new service called **Yelken Cloud** is being developed to let you easily create and manage your Yelken instances without worrying about the underlying infrastructure.
This month, decisions related to the infrastructure of Yelken Cloud and managing Yelken instances are made.
Besides that, basic functionalities of Yelken Cloud are implemented, such as creating a new Yelken instance and seamlessly logging into it.

## Final Thoughts
May was a very productive month for me in terms of carving the future of Yelken and its foundation.
While Yelken may not have received all the features I imagined at the beginning of this month, it still gained some important ones.
Now, it is time to implement the missing features next month.

## Learn more
Here are a few links to check out more about Yelken:

* Repository: [https://github.com/bwqr/yelken](https://github.com/bwqr/yelken)
* Book: [https://bwqr.github.io/yelken-book](https://bwqr.github.io/yelken-book)
* Blog: [https://bwqr.github.io/yelken-blog](https://bwqr.github.io/yelken-blog)
* Playground: [https://yelken-cms.netlify.app](https://yelken-cms.netlify.app)
* Examples: [https://github.com/bwqr/yelken/tree/main/examples](https://github.com/bwqr/yelken/tree/main/examples)
* Towards Yelken 0.1.0: [https://github.com/users/bwqr/projects/3](https://github.com/users/bwqr/projects/3)
* Discord server: [https://discord.gg/D4bfHr8neh](https://discord.gg/D4bfHr8neh)
