# A simplified Jira clone built with Angular, Akita and ng-zorro


You can check the storybook collection of components I wrote for Jira Clone ➡ [jira-storybook.trungk18.com](https://jira-storybook.trungk18.com/) 📕


## Working application

Check out the **live demo** -> https://jira.trungk18.com

![Jira clone built with Angular and Akita][demo]

## Storybook

### What is Storybook

Storybook helps you build UI components in isolation from your app's business logic, data, and context.
That makes it easy to develop hard-to-reach states. Save these UI states as **stories** to revisit during development, testing, or QA.

### Jira Clone Storybook

This is the collection of components that I wrote for [jira.trungk18.com][jira], includes:

- Avatar
- Breadcrumbs
- Button
- Input
- More to come...

Check out the **storybook demo** -> https://jira-storybook.trungk18.com/

![Jira clone built with Angular and Akita][demo-storybook]


This is an application that I've worked on during my spare time to experiment the new library : `Akita`, `TailwindCSS`, `ng-zorro`.


## Tech stack

![Tech logos][stack]

- [Angular CLI][cli]
- [Akita][akita] state management
- [NestJS][nestjs]
- UI modules:
  - [TailwindCSS][tailwind]
  - Angular CDK [drag and drop][cdkdrag]
  - [ng-zorro][ng-zorro] UI component: `tooltip`, `modal`, `select`, `icon` and more.
  - [ngx-quill][quill]
- [Netlify][netlify]
- [Heroku][heroku]

[cli]: https://cli.angular.io/
[akita]: https://datorama.github.io/akita/
[nestjs]: https://nestjs.com/
[tailwind]: https://tailwindcss.com/
[cdkdrag]: https://material.angular.io/cdk/drag-drop/overview
[ng-zorro]: https://ng.ant.design/docs/introduce/en
[quill]: https://github.com/KillerCodeMonkey/ngx-quill
[netlify]: https://www.netlify.com/
[heroku]: https://www.heroku.com/


### Application architecture

I have an AppModule that will import:

![Jira clone built with Angular and Akita - Application architecture][application-architecture]

- Angular needed modules such as `BrowserModule` and any module that need to run `forRoot`.
- The application core modules such as `AuthModule` that need to available on the whole platform.
- And I also configured the router to [lazy load any modules][lazy-load] only when I needed. Otherwise, everything will be loaded when I start the application.
  For instance, `LoginModule` when I open the URL at `/login` and `ProjectModule` when the URL is `/project`. Inside each modules, I could import whatever modules that are required. Such as I need the `JiraControlModule` for some custom UI components for the `ProjectModule`

### Simple data interaction flow

As I am using [Akita][akita] state management, I follow the Akita documentation for the data flow. I found it is simple to understand comparing with ngrx terms (`reducer`, `selector`, `effect`)

![Jira clone built with Angular and Akita - Simple data interaction flow][interaction-data-flow]

I set up a [project state with initial data][project-store]. The main heavy lifting part I think is the [project service][project-service], it contains all the interacting with [project store][project-store]. Such as after fetching the project successfully, I update the store immediately inside the service itself. The last lego block was to expose the data through [project query][project-query]. Any components can start to inject [project query][project-query] and consume data from there.

If you are using ngrx, you have to dispatch an action when you started fetching the project, and then there is an effect somewhere that was detached from your context need to handle the action, send a request to the API server. And finally, the effect will tell whether the data was successfully fetched or not. <u>There is nothing wrong with ngrx approach</u>, it is just too much concept and layer that you need to understand. To be honest, I used to afraid of integrating ngrx in my project because of the unnecessary complexity it would bring.


###  Angular application and simple Nest API

-  Proven, scalable, and easy to understand project structure
-  Simple drag and drop kanban board
-  Add/update issue
-  Search/filtering issues
-  Add comments