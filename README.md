# java-model

[![npm version](https://img.shields.io/npm/v/java-model.svg?style=flat-square)](https://www.npmjs.com/package/java-model)

Provides high-level access to the Java type model, based on [java-ast](https://github.com/pascalgn/java-ast).

## Usage

```java
class A {
    private int i;
}

record B(String s) {
}

enum C { C1, C2 }
```

### Array of Sources

```typescript
import { readFileSync } from "node:fs";
import { parse } from "java-model";

const files = ["input.java"];
const sources = files.map((file) => readFileSync(file, "utf8"));
const project = parse(sources);

project.visitTypes((type) => {
   console.log(type.name);
   console.log(type.qualifiedName);
   console.log(type.properties());
});

project.compilationUnits.forEach(type => {
   console.log(type.imports);
});

project.typeDeclarations.forEach(type => {
   console.log(type.name);
   console.log(type.qualifiedName);
   console.log(type.properties());
});
```

### Provide a Read Function

```typescript
import { readFileSync } from "node:fs";
import { parse } from "java-model";

const project = parse({
    files: ["input.java"],
    read: file => readFileSync(file, "utf8")
});

project.visitTypes(type => {
   console.log(type.name);
   console.log(type.qualifiedName);
   console.log(type.properties());
});
```

### Provide an Async Read Function

```typescript
import { readFile } from "node:fs/promises";
import { parse } from "java-model";

const project = parse({
    files: ["input.java"],
    readAsync: file => readFile(file, "utf8")
});

project.visitTypes(type => {
   console.log(type.name);
   console.log(type.qualifiedName);
   console.log(type.properties());
});
```

## License

[MIT](LICENSE)
