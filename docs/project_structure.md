# Project structure

Atomic structure is what define the shape of our app structures. The term "Atomic Design" refers to a methodology for creating design systems and user interfaces by breaking down the design into smaller, more manageable components. This methodology was introduced by Brad Frost. The idea behind Atomic Design is inspired by the way chemistry represents.

<small style="color: red">Press down to see examples.</small>




### Angular structure

Here is a sample of Angular tree

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
│   │   │   ├── auth
│   │   │   │   ├── auth.module.ts
│   │   │   │   ├── auth-routing.module.ts
│   │   │   │   └── components
│   │   │   │       ├── accept-invite
│   │   │   │       │   ├── accept-invite.component.html
│   │   │   │       │   ├── accept-invite.component.scss
│   │   │   │       │   └── accept-invite.component.ts
│   │   │   │       ├── index.ts
│   │   │   │       ├── login
│   │   │   │       │   ├── login.component.html
│   │   │   │       │   ├── login.component.scss
│   │   │   │       │   └── login.component.ts
│   │   │   │       ├── register
│   │   │   │       │   ├── register.component.html
│   │   │   │       │   ├── register.component.scss
│   │   │   │       │   └── register.component.ts
│   │   │   │       ├── reset-password
│   │   │   │       │   ├── reset-password.component.html
│   │   │   │       │   ├── reset-password.component.scss
│   │   │   │       │   └── reset-password.component.ts
│   │   │   │       ├── sso-callback-handler.component.ts
│   │   │   │       └── token-register
│   │   │   │           ├── token-register.component.html
│   │   │   │           ├── token-register.component.scss
│   │   │   │           └── token-register.component.ts
```



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