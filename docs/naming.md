## Naming conventions

Naming conventions in programming refer to a set of rules and guidelines for choosing meaningful and consistent names for variables, functions, classes, and other identifiers within a software project. These conventions help improve code readability, maintainability, and collaboration among team members.

<small style="color: red">Press down to see examples.</small>




### Args (BE)

`Args` define our GQL input contract. Those args has special naming as follow:

- File name as (kebab-case): **[ADMIN?]-[ACTION_NAME].args.ts**
  - e.g: **admin-create-organization.args.ts**
- Input class name as (PascalCase): **[Admin?][action_name]Input**
  - e.g: **AdminAttachOrganizationToUserInput**
- Args class name as (PascalCase): **[Admin?][action_name]Args**
  - e.g: **AdminAttachOrganizationToUserArgs**

_Admin_ name is optional upon the usage. If the arg/controller/service/resolver used in admin-ui, we prefix _admin_ otherwise, it is used in learner-ui.

We need both _Args_ and _Input_ where args define Input object with decorator _@ArgsType()_ and Input define Input SDL (Schema Definition Language) in GQL using _@InputType()_.



### Args example:

```ts
import { ArgsType, Field, ID, InputType } from '@nestjs/graphql';
import { Type } from 'class-transformer';
import { IsMongoId, IsNotEmpty, ValidateNested } from 'class-validator';
import { UserAuthorizationInput } from './user-authorization.args';

@InputType()
export class AdminAttachOrganizationToUserInput {
  @IsMongoId()
  @IsNotEmpty()
  @Field(() => ID)
  id: string;

  @Field(() => [UserAuthorizationInput])
  authorizations: UserAuthorizationInput[];
}

@ArgsType()
export class AdminAttachOrganizationToUserArgs {
  @Field(() => AdminAttachOrganizationToUserInput)
  @Type(() => AdminAttachOrganizationToUserInput)
  @ValidateNested()
  input: AdminAttachOrganizationToUserInput;
}
```



### Models (BE)

`Models` Has both DTOs and GQL Data models. Where DTO is remap **Mostly** from from DB document to an object that clients needs.

- File name as (kebab-case): **[MODEL_NAME].model.ts** e.g:
  - **organization.model.ts**
- Class object type name as (PascalCase): **[MODEL_NAME]Model**
  - e.g: **OrganizationModel**

GQL Model is converted into SDL (Schema Definition Language) using decorator _@ObjectType()_.



### Resolver & Services (BE)

`Resolvers` are the main interface between client and BE services.

- File name as (kebab-case): **[ADMIN?]-[MODEL_NAME].resolver.ts**
  - e.g: **admin-organization.resolver.ts**
- Class object type name as (PascalCase): **[ADMIN?]-[MODEL_NAME].resolver** 
  - e.g: **AdminORganizationResolver**

GQL Model is converted into SDL (Schema Definition Language) using decorator _@ObjectType()_.


