# nestjs-crud-mongoose
Mongoose/Typegoose service adapter for [@nestjsx/crud](https://github.com/nestjsx/crud)

> Nest.js + typegoose video (chinese):
> 
> Nest.js + Typegoose 中文视频教程请移步哔哩哔哩全栈之巅:
>
> https://space.bilibili.com/341919508


## How to

### Install

```bash
yarn add nestjs-crud-mongoose
# or
npm i nestjs-crud-mongoose
```

### Create a service based on a mongoose/typegoose model
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

OR

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

### Inject `UsersService` to your `UsersController`:

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