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
