## DB References.

Simply if you have an ID fields referencing another document in another collection, always store them as ObjectId. WHY??

- _id is always ObjectId. If you use another field name in another collection, it would make sense to be ObjectId so you can use population.
- For the sake of defining virtual fields.

```ts
import { Prop, Schema, SchemaFactory } from '@nestjs/mongoose';
import { ContentfulCollectionType } from '@xu-group/nest/contentful';
import { HydratedDocument, Model, Types } from 'mongoose';
import { OrganizationDocument } from '../organization/organization.schema';
import { UserDocument } from '../user/user.schema';
import {
  ElementProgressDocument,
  ElementProgressSchema,
} from './element-progress.schema';
import { ProgressState } from './progress-state.enum';

@Schema({
  toObject: { virtuals: true },
  toJSON: { virtuals: true },
  id: true,
  timestamps: true,
})
export class Progress {
  @Prop({ type: Types.ObjectId, required: true, rel: 'User' })
  userId: Types.ObjectId;

  @Prop({ type: Types.ObjectId, required: true, rel: 'Organization' })
  organizationId: Types.ObjectId;

  [...]
}

export type ProgressDocument = HydratedDocument<
  Progress & {
    userRef?: UserDocument;
    organizationRef?: OrganizationDocument;
  }
>;
export type ProgressDbModel = Model<
  Progress & {
    userRefs?: UserDocument[];
    organizationRefs?: OrganizationDocument[];
  }
>;

export const ProgressSchema = SchemaFactory.createForClass(Progress);
ProgressSchema.virtual('id').get(function () {
  return this._id.toHexString();
});
ProgressSchema.index({ userId: 1 });
ProgressSchema.index({ organizationId: 1 });

ProgressSchema.virtual('userRef', {
  ref: 'User',
  localField: 'userId',
  foreignField: '_id',
  justOne: true,
});
ProgressSchema.virtual('organizationRef', {
  ref: 'Organization',
  localField: 'organizationId',
  foreignField: '_id',
  justOne: true,
});
```