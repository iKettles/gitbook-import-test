# Table of contents

* [Welcome to the internal Monopoly-as-a-Service Docs](./internal/README.md)
* [API](internal/api/README.md)
  * ```yaml
    type: builtin:openapi
    props:
      models: true
    dependencies:
      spec:
        ref:
          kind: openapi
          spec: monopoly-internal-api-reference
    ```
