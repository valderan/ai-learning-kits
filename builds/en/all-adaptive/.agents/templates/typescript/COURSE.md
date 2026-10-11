<!-- Example for TypeScript: copy this file and replace the topics with your own. -->

# Course: TypeScript — types and backend

## Learning goal

Write type-safe TypeScript: utilities and an HTTP API on Node, with tests; the vector is backend development for work in a product team.

## Student context

- Current level: confident in JavaScript, has not written TypeScript
- Why learning: work
- Time and pace: 4 hours per week
- Format: practice in this project, strict compiler mode from the first topic
- Practice: self-study

## What you will be able to do

- describe data with types, interfaces and generics
- work safely with async/await and errors
- write tests with vitest and keep the project in strict mode
- accept and validate API data at the application boundary

## Out of scope

- frontend frameworks, databases, deployment

## When a topic counts as done

- the assignment works, `npm test` passes, `tsc --noEmit` reports no errors
- the student has explained the solution in their own words

## Program

### Module 1. Type basics

1. Primitives, type inference, annotations
2. Union, literal, narrowing
3. Functions: parameters, overloads, this

### Module 2. Objects and generics

4. Object types, interfaces and type
5. Generics and constraints
6. Utility types: Partial, Pick, Record

### Module 3. Classes and modules

7. Classes, access modifiers, implements
8. ES modules and strict settings in tsconfig

### Module 4. Asynchrony

9. Promise, async/await
10. Error handling and unknown types
11. Parallel requests and cancellation

### Module 5. Tests and tooling

12. vitest: tests, mocks, coverage
13. ESLint, formatting, building with tsc

### Module 6. Practice: HTTP API

14. Routing and handlers on Node
15. Data validation with zod
16. Typing responses and API tests

## Materials

- TypeScript Handbook — https://www.typescriptlang.org/docs/handbook/intro.html
- TypeScript roadmap — https://roadmap.sh/typescript
- vitest — https://vitest.dev/guide/

---

Updated: 2026-10-10 (example; check the current TypeScript and library versions before use)
