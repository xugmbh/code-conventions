## Project structure

Atomic structure is what define the shape of our app structures. The term "Atomic Design" refers to a methodology for creating design systems and user interfaces by breaking down the design into smaller, more manageable components. This methodology was introduced by Brad Frost. The idea behind Atomic Design is inspired by the way chemistry represents.

<small style="color: red">Press down to see examples.</small>




### Nest structure

```bash [8-26]
├── src
│   ├── app
│   │   ├── app.controller.spec.ts
│   │   ├── app.controller.ts
│   │   ├── app.module.ts
│   │   ├── app.service.spec.ts
│   │   ├── app.service.ts
│   │   ├── certificate
│   │   │   ├── args
│   │   │   │   └── generate-certificate.args.ts
│   │   │   ├── certificate.module.ts
│   │   │   ├── contentful.http
│   │   │   ├── mocks
│   │   │   │   └── collection.json
│   │   │   ├── models
│   │   │   │   └── certificate.model.ts
│   │   │   ├── resolvers
│   │   │   │   └── certificate.resolver.ts
│   │   │   ├── services
│   │   │   │   ├── certificate-check-cases.service.ts
│   │   │   │   └── certificate.service.ts
│   │   │   ├── templates
│   │   │   │   ├── default.template.ejs
│   │   │   │   └── index.ts
│   │   │   └── tests
│   │   │       └── certificate.spec.ts
│   │   ├── assessment
│   │   │   ├── args
│   │   │   │   ├── admin-find-assessments.args.ts
│   │   │   │   ├── assessment-assignment
│   │   │   │   ├── find-assessment-results.args.ts
│   │   │   │   ├── find-organization-assessments.args.ts
│   │   │   │   ├── finish-assessment-result.args.ts
│   │   │   │   └── init-assessment-result.args.ts
│   │   │   ├── assessment.http
│   │   │   ├── assessment.module.ts
│   │   │   ├── models
│   │   │   │   ├── assessment-assignment.model.ts
│   │   │   │   ├── assessment-result.ts
│   │   │   │   ├── dto
│   │   │   │   └── learner-assessment.model.ts
│   │   │   ├── resolvers
│   │   │   │   ├── admin-assessment-assignment.resolver.ts
│   │   │   │   ├── admin-assessment.resolver.ts
│   │   │   │   └── learner-assessment.resolver.ts
│   │   │   ├── services
│   │   │   │   ├── admin-assessment-assignment.service.ts
│   │   │   │   ├── assessment-result.service.ts
│   │   │   │   ├── assessment-result-synchronise.service.ts
│   │   │   │   ├── assessment-validator.service.ts
│   │   │   │   └── learner-assessment.service.ts
│   │   │   └── tests
│   │   │       ├── assessment.spec.ts
│   │   │       └── mocks
│   │   ├── common
│   │   │   ├── args
│   │   │   │   └── gql-pagination.args.ts
│   │   │   ├── decorators
│   │   │   │   └── public-api.decorator.ts
│   │   │   ├── guards
│   │   │   │   └── organization.guard.ts
│   │   │   ├── models
│   │   │   │   ├── list-metadata.model.ts
│   │   │   │   └── timestamp.model.ts
│   │   │   └── utils
│   │   │       └── common-user.util.ts
```




### Angular structure

The Service-based (Domain-driven Design) Structure, also known as a Domain-driven Design (DDD) structure, is an organizational approach to software architecture that revolves around business domains and the concept of services. Domain-driven design is a set of principles and practices for building complex systems.

```bash [11-37]
├── src
│   ├── app
│   │   ├── app.component.html
│   │   ├── app.component.scss
│   │   ├── app.component.spec.ts
│   │   ├── app.component.ts
│   │   ├── app.module.ts
│   │   ├── app-routing.module.ts
│   │   ├── constant.ts
│   │   ├── graphql.module.ts
│   │   ├── modules
│   │   │   ├── assessments
│   │   │   │   ├── assessments.module.ts
│   │   │   │   └── components
│   │   │   ├── auth
│   │   │   │   ├── auth.module.ts
│   │   │   │   ├── auth-routing.module.ts
│   │   │   │   └── components
│   │   │   ├── catalogue
│   │   │   │   ├── catalogue.module.ts
│   │   │   │   └── components
│   │   │   ├── collections
│   │   │   │   ├── collections.component.html
│   │   │   │   ├── collections.component.scss
│   │   │   │   ├── collections.component.ts
│   │   │   │   ├── collections.module.ts
│   │   │   │   ├── collections-routing.module.ts
│   │   │   │   └── components
│   │   │   ├── dashboard
│   │   │   │   ├── components
│   │   │   │   └── dashboard.module.ts
│   │   │   ├── home
│   │   │   │   ├── components
│   │   │   │   ├── home.module.ts
│   │   │   │   ├── home-routing.module.ts
│   │   │   │   └── resolver
│   │   │   ├── library
│   │   │   │   ├── components
│   │   │   │   ├── library.component.html
│   │   │   │   ├── library.component.scss
│   │   │   │   ├── library.component.ts
│   │   │   │   ├── library.module.ts
│   │   │   │   └── library-routing.module.ts
│   │   │   ├── live-sessions
│   │   │   │   ├── components
│   │   │   │   ├── live-sessions.component.html
│   │   │   │   ├── live-sessions.component.scss
│   │   │   │   ├── live-sessions.component.ts
│   │   │   │   ├── live-sessions.module.ts
│   │   │   │   └── live-sessions-routing.module.ts
│   │   │   ├── organizations
│   │   │   │   ├── components
│   │   │   │   ├── guards
│   │   │   │   └── organizations.module.ts
│   │   │   └── workspaces
│   │   │       ├── components
│   │   │       └── workspaces.module.ts
│   │   └── shared
│   │       ├── components
│   │       │   ├── calendar
│   │       │   ├── collection-card
│   │       │   ├── empty-card
│   │       │   ├── index.ts
│   │       │   ├── library-card
│   │       │   └── sidebar-filter
│   │       ├── directive
│   │       │   ├── click-outside
│   │       │   ├── index.ts
│   │       │   ├── read-more
│   │       │   └── swiper
│   │       ├── guards
│   │       │   └── user-role.guard.ts
│   │       ├── models
│   │       │   ├── collection.model.ts
│   │       │   ├── collection-progress.model.ts
│   │       │   ├── element-progress.model.ts
│   │       │   └── library-progress.model.ts
│   │       ├── modules
│   │       │   └── theme
│   │       ├── pipes
│   │       │   ├── date-to-month
│   │       │   ├── empty
│   │       │   ├── html-rendered
│   │       │   ├── index.ts
│   │       │   ├── marked
│   │       │   ├── min-to-hrs
│   │       │   ├── not
│   │       │   └── safe
│   │       ├── services
│   │       │   ├── analytics.service.ts
│   │       │   ├── assessment.service.ts
│   │       │   ├── category.service.ts
│   │       │   ├── collection.service.ts
│   │       │   ├── library.service.ts
│   │       │   ├── navigate.service.ts
│   │       │   └── sessions.service.ts
│   │       └── shared.module.ts
```