# nestjs-crud-mongoose
mongoose service adapter for @nestjsx/crud


## How to

`/src/users/users.service.ts`

```ts
// for typegoose users
import { User } from "../../common/users/user.model";
import { Injectable, Inject } from "@nestjs/common";
import { ModelType } from "@typegoose/typegoose/lib/types";
import { MongooseCrudService } from "./mongoose-crud.service";

@Injectable()
export class UsersService extends MongooseCrudService<User>{
  constructor(@Inject('UserModel') public model: ModelType<User>) {
    super(model)
  }
}
```
### OR
```ts
// for mongoose users
import { User } from "../../common/users/user.model";
import { Injectable, Inject } from "@nestjs/common";
import { Model } from "mongoose";
import { MongooseCrudService } from "./mongoose-crud.service";

@Injectable()
export class UsersService extends MongooseCrudService<User>{
  constructor(@Inject('UserModel') public model: Model<User>) {
    super(model)
  }
}

```

Then, inject `UsersService` to your `UsersController`:

```ts
@Crud({
  // ...
})
export class UsersController {
  constructor(public service: UsersService) { }
}
```


## Thanks to

- https://github.com/nestjsx/crud
- https://github.com/nestjsx/crud/tree/master/packages/crud-typeorm

## Related docs
- https://github.com/nestjsx/crud/wiki/ServiceTypeorm