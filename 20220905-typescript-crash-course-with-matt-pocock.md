[open in Gitpod](https://gitpod.io/#https://github.com/total-typescript/beginners-typescript)

[video crash course](https://www.youtube.com/watch?v=p6dO9u0M7MQ)

## 01-number

problem
```ts
import { expect, it } from "vitest";


export const addTwoNumbers = (a, b) => {
  return a + b;
};

it("Should add the two numbers together", () => {
  expect(addTwoNumbers(2, 4)).toEqual(6);
  expect(addTwoNumbers(10, 10)).toEqual(20);
});
```

solution
```ts

export const addTwoNumbers = (a: number, b: number) => {
  return a + b;
};
```
## 02-object-param

problem
```ts
import { expect, it } from "vitest";

export const addTwoNumbers = (params) => {
  return params.first + params.second;
};

it("Should add the two numbers together", () => {
  expect(
    addTwoNumbers({
      first: 2,
      second: 4,
    }),
  ).toEqual(6);

  expect(
    addTwoNumbers({
      first: 10,
      second: 20,
    }),
  ).toEqual(30);
});


```

solution 1
```ts
export const addTwoNumbers = (params: { first: number; second: number }) => {
  return params.first + params.second;
};
```

solution 2
```ts
type AddTwoNumbersArgs = {
  first: number;
  second: number;
};

export const addTwoNumbers = (params: AddTwoNumbersArgs) => {
  return params.first + params.second;
};
```

solution 3
```ts
interface AddTwoNumbersArgs {
  first: number;
  second: number;
}

export const addTwoNumbers = (params: AddTwoNumbersArgs) => {
  return params.first + params.second;
};
```

## 03-optional-properties

problem
```ts
import { expect, it } from "vitest";

# 1
export const getName = (params: { first: string; last: string }) => {
  if (params.last) {
    return `${params.first} ${params.last}`;
  }
  return params.first;
};

it("Should work with just the first name", () => {
  const name = getName({
    first: "Matt",
  });

  expect(name).toEqual("Matt");
});

it("Should work with the first and last name", () => {
  const name = getName({
    first: "Matt",
    last: "Pocock",
  });

  expect(name).toEqual("Matt Pocock");
});
```

solution   ( just a ? mark, woala)
```ts
# 1
export const getName = (params: { first: string; last?: string }) => {
```

## 04-optional-params

problem
```ts
import { expect, it } from "vitest";

export const getName = (first: string, last: string) => {
  if (last) {
    return `${first} ${last}`;
  }
  return first;
};

it("Should work with just the first name", () => {
  const name = getName("Matt");

  expect(name).toEqual("Matt");
});

it("Should work with the first and last name", () => {
  const name = getName("Matt", "Pocock");

  expect(name).toEqual("Matt Pocock");
});

```

solution
```ts
export const getName = (first: string, last?: string) => {
  if (last) {
    return `${first} ${last}`;
  }
  return first;
};
```

one more thing
```ts
export const getName = (first: string, ...otherNames: string[]) => {
  if (otherNames[0]) {
    return `${first} ${otherNames[0]}`;
  }
  return first;
};
```

## 05-assigning-types-to-variables

problem
```ts
import { expect, it } from "vitest";

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
```

solution
```ts
import { expect, it } from "vitest";

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
const defaultUser: User = {
  id: 1,
  firstName: "Matt",
  lastName: "Pocock",
  isAdmin: true,
};

```

one more thing
```ts
const defaultUser = {
  id: 1,
} as User;
```

## 06-unions

problem
```ts
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

export const defaultUser: User = {
  id: 1,
  firstName: "Matt",
  lastName: "Pocock",
  role: "I_SHOULD_NOT_BE_ALLOWED",
};

```

solution 
```ts
role: "admin" | "user" | "super-admin";
```

one more thing
```ts
type User3 = {
    id: number;
    firstName: string;
    lastName: string;
} & (
    | { role: "user" }
    | { role: "admin"; adminPassword: string }
    | { role: "super-admin"; superAdminPassword: string }
);

```

one more thing
```ts
type User3 = {
    id: number;
    firstName: string;
    lastName: string;
} & UserRoleAttributes;

type UserRoleAttributes =
    | { role: "user" }
    | { role: "admin"; adminPassword: string }
    | { role: "super-admin"; superAdminPassword: string };

type Role = UserRoleAttributes["role"];

interface User {
  id: number;
  firstName: string;
  lastName: string;
  role: Role;
}
```
