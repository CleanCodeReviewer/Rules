# CCR Rules Repository

Official rules repository for [Clean Code Reviewer](https://github.com/CleanCodeReviewer/CleanCodeReviewer).

## Structure

```
ccr-rules/
└── src/
    ├── base.yml                # Universal clean code principles
    ├── google/
    │   ├── python.yml
    │   ├── javascript.yml
    │   ├── typescript.yml
    │   ├── go.yml
    │   ├── java.yml
    │   ├── cpp.yml
    │   ├── csharp.yml
    │   ├── swift.yml
    │   ├── objc.yml
    │   ├── shell.yml
    │   ├── html-css.yml
    │   └── ...
    ├── airbnb/
    │   ├── javascript.yml
    │   └── react.yml
    ├── uber/
    │   └── go.yml
    ├── microsoft/
    │   └── csharp.yml
    └── yourcompany/
        └── your-rules.yml
```

**All namespaces are equal.** There's no hierarchy between organizations - Google's rules aren't more "official" than yours.

## Usage

```bash
# Download rules
ccr add base                    # → .cleancoderules/base.yml
ccr add google/python           # → .cleancoderules/community/google/python.yml
ccr add airbnb/javascript       # → .cleancoderules/community/airbnb/javascript.yml
ccr add yourcompany/standards   # → .cleancoderules/community/yourcompany/standards.yml
```

## Enforcement Levels

Rules use RFC 2119-inspired enforcement levels to indicate strictness:

| Level        | Meaning                                                    |
| ------------ | ---------------------------------------------------------- |
| `MUST`       | Absolute requirement. Violations should always be flagged. |
| `SHOULD`     | Recommended practice. Exceptions need justification.       |
| `MAY`        | Optional. At developer's discretion.                       |
| `SHOULD_NOT` | Discouraged practice. Exceptions need justification.       |
| `MUST_NOT`   | Absolute prohibition. Never acceptable.                    |

### Examples

```yaml
naming:
  class_names:
    enforcement: MUST
    value: PascalCase

functions:
  max_lines:
    enforcement: SHOULD
    value: 20

comments:
  trailing_commas:
    enforcement: MAY
    value: "Use trailing commas in multi-line structures"

error_handling:
  bare_except:
    enforcement: MUST_NOT
    value: "Never use bare except clauses"
```

## Available Rules

### Base

| Rule   | Description                     |
| ------ | ------------------------------- |
| `base` | Universal clean code principles |

### By Namespace

| Namespace   | Rules                                                                                                                                                                       | Description                     |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- |
| `google`    | `python`, `javascript`, `typescript`, `go`, `java`, `cpp`, `csharp`, `swift`, `objc`, `shell`, `html-css`, `json`, `xml`, `markdown`, `r`, `lisp`, `vimscript`, `angularjs` | Google style guides             |
| `airbnb`    | `javascript`, `react`                                                                                                                                                       | Airbnb style guides             |
| `uber`      | `go`                                                                                                                                                                        | Uber Go style guide             |
| `microsoft` | `csharp`                                                                                                                                                                    | Microsoft C# coding conventions |

## Contributing

1. Fork this repository
2. Create your namespace: `yourname/` or `yourcompany/`
3. Add your rules as YAML files
4. Submit a PR

### Rule Format

Rules are YAML files with a `_meta` header and structured rule definitions:

```yaml
# Rule file header
_meta:
  name: my-rule
  language: python
  tags: [security, style]
  source: "https://example.com/style-guide"

# Rule definitions
naming:
  class_names:
    enforcement: MUST
    value: PascalCase
    good: |
      class UserService:
          pass
    bad: |
      class user_service:
          pass

functions:
  max_arguments:
    enforcement: SHOULD
    value: 3
```

### Schema

Every rule must have these fields:

| Field         | Required | Type   | Description                                       |
| ------------- | -------- | ------ | ------------------------------------------------- |
| `enforcement` | Yes      | enum   | `MUST`, `SHOULD`, `MAY`, `SHOULD_NOT`, `MUST_NOT` |
| `value`       | Yes      | any    | The rule value (string, number, or list)          |
| `good`        | No       | string | Example of correct code                           |
| `bad`         | No       | string | Example of incorrect code                         |

### Guidelines

- Rules should be actionable and specific
- Include `good:` and `bad:` examples where helpful
- Explain WHY, not just WHAT
- Keep rules focused (one concept per rule)
- Use appropriate enforcement levels:
  - `MUST` for naming conventions, security requirements
  - `SHOULD` for best practices, style recommendations
  - `MAY` for optional patterns
  - `MUST_NOT` for dangerous practices (eval, panics, etc.)

## License

MIT
