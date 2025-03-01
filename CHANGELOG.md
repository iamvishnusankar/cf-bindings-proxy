# cf-bindings-proxy

## 0.2.4

### Patch Changes

- 000367c: Fix retrieving undefined array value at index returning proxy func instead of undefined.

## 0.2.3

### Patch Changes

- ab8484a: Fix D1Result undefined properties returning truthy value.

## 0.2.2

### Patch Changes

- 5289f47: Fix accessing an instance of a binding through a variable multiple times interfacing on the same instance - create a new proxy instance for each time the binding is accessed.

  The below code is a good example of this fix. Previously, each time an action was performed using the `d1` variable, it was always interfacing with the same instance. This change fixes that, so that each time the `d1` variable is accessed below, it is interfacing with an entirely new instance of the binding. This prevents different actions on a binding via a variable from breaking each other.

  ```ts
  const insertQuery = [
  	`INSERT INTO comments (author, body, post_slug) VALUES ('Markus', 'Hello there!', ?);`,
  	`INSERT INTO comments (author, body, post_slug) VALUES ('Kristian', 'Great post!', ?);`,
  ];

  const d1 = binding<D1Database>('D1');

  const statements = insertQuery.map((query) => d1.prepare(query).bind('hello-world'));
  await d1.batch(statements);
  ```

## 0.2.1

### Patch Changes

- 0c387c0: Pass a compatibility date by default.
- 0c387c0: Log information about the tool to the console on startup.

## 0.2.0

### Minor Changes

- 0f37886: Initial support for running a proxy for bindings with D1/KV/R2.
