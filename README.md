# vue-test-utils-classes

Repo to reproduce typescript error

## Steps to reproduce

```
npm install

npm run serve
```

## what happens
typescript yield an error:

```
ERROR in /Users/yawenxiao/Personal/vue-test-utils-classes/tests/unit/HelloWorld.spec.ts
10:30 Property 'includes' does not exist on type 'void | string[]'.
  Property 'includes' does not exist on type 'void'.
     8 |       propsData: { msg },
     9 |     });
  > 10 |     expect(wrapper.classes().includes('a')).toBe(false);
       |                              ^
    11 |   });
    12 | });
    13 |
Version: typescript 2.9.1
```
## how to solve
I read the [source code](https://github.com/vuejs/vue-test-utils/blob/dev/packages/test-utils/types/index.d.ts#L59) and find the type definition of the `classes()` method is this:

```
classes(): Array<string> | void
```

Maybe because the return value could be void so it does not have a `includes` method.

When I change it to :
```
classes(): Array<string>
```
the error disappears and everything works ok.
