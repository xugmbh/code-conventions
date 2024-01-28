# DTOs (Data Transfer Objects):
DTOs to define the shape of data being transferred between client and server. They are meant to be generic as much as possible.


- Since it is related to server, avoid as much as possible having extra mapping in the FE. If there is a hurdle related data shape, it would be always suitable to have a proper structure in the BE. FE should be visual representation mostly.
- Avoid having logic business inside those DTOs. As they are multi usage mapping functions, any extra logic can easily break the contract of the function. (Contract means the inputs of the functions)

- If the data model needs to be reshaped in the FE for a **critical reasons** of UI, set the main source data in a service related to the module and create another mapping inside the same service. Avoid having the mapping in different place.

<small style="color: red">Press down to see examples.</small>



### A good DTO example:

- This is a good example.
- Always think about optional fields what would be if they are empty? Does it break something? Should we fallback to a specific value?
- No logic has been set but only mapping.
- Should return what the FE expect.
- Always be careful from nested DTOs. Think about them if they are not presented in the main object. "get" from lodash id your friend here.

```ts [12-16]
import { RichTextModel, contentfulAssetDto } from '@xu-group/nest/contentful';
import { Asset as ContentfulAsset } from 'contentful';
import { get } from 'lodash';
import { ContentfulSessionEntry } from '../types/contentful-session-entry.type';
import { BaseSessionModel } from './base-contentful-session.model';

export function sessionDto(
  contentfulSessionItem: ContentfulSessionEntry
): BaseSessionModel {
  const id = get(contentfulSessionItem, 'sys.id', '') as string;
  const name = get(contentfulSessionItem, 'fields.name', '') as string;
  const title = get(contentfulSessionItem, 'fields.title', '') as string;
  const duration = get(contentfulSessionItem, 'fields.duration', 0) as number;
  const embed = get(contentfulSessionItem, 'fields.embed', '') as string;
  const createdAt = contentfulSessionItem.sys.createdAt;
  const updatedAt = contentfulSessionItem.sys.updatedAt;
  const locale = contentfulSessionItem.sys.locale || 'en-US';

  const description = get(contentfulSessionItem, 'fields.description', {
    value: '',
    nodeType: '',
    content: [],
  }) as RichTextModel;

  const speakerName = get(
    contentfulSessionItem,
    'fields.speakerName',
    ''
  ) as string;

  const images = (
    get(contentfulSessionItem, 'fields.images', []) as ContentfulAsset[]
  ).map((image) => contentfulAssetDto(image));

  const contentfulMedia = get(
    contentfulSessionItem,
    'fields.media'
  ) as ContentfulAsset;
  const media = contentfulMedia && contentfulAssetDto(contentfulMedia);

  const contentfulSpeakerImage = get(
    contentfulSessionItem,
    'fields.speakerImage'
  ) as ContentfulAsset;
  const speakerImage =
    contentfulSpeakerImage && contentfulAssetDto(contentfulSpeakerImage);

  const speakerIntro = get(
    contentfulSessionItem,
    'fields.speakerIntro',
    ''
  ) as string;

  const eventDateTime = get(
    contentfulSessionItem,
    'fields.eventDateTime',
    ''
  ) as string;

  const participationLimit = get(
    contentfulSessionItem,
    'fields.participationLimit',
    0
  ) as number;

  return {
    id,
    name,
    locale,
    title,
    description,
    images,
    speakerName,
    speakerImage,
    speakerIntro,
    embed,
    eventDateTime,
    participationLimit,
    duration,
    media,
    createdAt,
    updatedAt,
  };
}
```




### A bad DTO example:

Let us assume the following scenario here:

```ts
import { User as ClerkUser } from '@clerk/clerk-sdk-node';
import {
  UserAuthorizationDocument,
  UserDocument,
} from '../../database/user/user.schema';
import {
  OrganizationDocument,
} from '../../database/organization/organization.schema';
import { AuthorizationModel, ClerkInsights, UserModel } from './user.model';
import { organizationDto } from './organization.model';

export function userDto(
  doc: Partial<UserDocument>,
  organization: OrganizationDocument
): UserModel {
  return {
    id: doc.id,
    firstName: doc.firstName,
    lastName: doc.lastName,
    email: doc.email,
    iamReference: doc.iamReference,
    allowedListIdentifierIamRef: doc.allowedListIdentifierIamRef,
    invitationRef: doc.invitationRef,
    role: doc.role,
    locale: doc.locale,
    authorizations: userAuthorizationDto(doc.authorizations),
    registrationComplete: doc.registrationComplete,
    projects: doc.projects,
    lastSeen: doc.lastSeen,
    createdAt: doc.createdAt,
    updatedAt: doc.updatedAt,
    registeredAt: doc.registeredAt,
    userOrganizations: organizationDto(organization),
  };
}
```

- This is an explicit coupling with both modules which will force developer to use it only when having both documents [user, organization].
- The same applicable if you set logic inside DTOs functions. Business logic code always belong to services.