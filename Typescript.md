## Check Merged tsconfig Configuration

When working with multiple TypeScript configuration files that use `extends`, it can be difficult to know the final merged configuration that TypeScript uses.

The `--showConfig` option displays the resolved TypeScript configuration after applying all inherited configs.

## Usage

Run:

```bash
npx tsc -p tsconfig.ng-doc.json --showConfig
```
