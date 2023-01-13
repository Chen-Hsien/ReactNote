# TypeScript
1. Any type Error
```typescript
export const addTwoNumbers = (a, b) => {
  return a + b;
};

export const addTwoNumbers = (a:number, b:number) => {
  return a + b;
};
```
2. Object Params
```typescript
interface params{
  first: number,
  second: number
}
export const addTwoNumbers = (params :params) => {
  return params.first + params.second;
};
```
3. Set Optional Properties
```Typescript
export const getName = (first: string, last?: string) => {
  if (last) {
    return `${first} ${last}`;
  }
  return first;
};
//this must to pass last
export const getName = (first: string, last: string | undifined) => {
  if (last) {
    return `${first} ${last}`;
  }
  return first;
};
```
4. Assigning Types to Variables
```Typescript
interface User {
  id: number;
  firstName: string;
  lastName: string;
  isAdmin: boolean;
}

/**
 * How do we ensure that defaultUser is of type User
 * at THIS LINE - not further down in the code?
 */
const defaultUser = {};

const getUserId = (user: User) => {
  return user.id;
};

it("Should get the user id", () => {
  expect(getUserId(defaultUser)).toEqual(1);
});
--------------
const defaultUser:User = {
  id:1,
  firstName:'test',
  lastName:'cc',
  isAdmin:true
};

const getUserId = (user: User) => {
  return user.id;
};

it("Should get the user id", () => {
  expect(getUserId(defaultUser)).toEqual(1);
});
```

5. Constraining Value Types
```
interface User {
  id: number;
  firstName: string;
  lastName: string;
  /**
   * How do we ensure that role is only one of:
   * - 'admin'
   * - 'user'
   * - 'super-admin'
   */
  role: string;
}
-------------
interface User {
  id: number;
  firstName: string;
  lastName: string;
  role: 'admin'|'user'|'super-admin';
}
```

6. 
