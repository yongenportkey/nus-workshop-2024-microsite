---
sidebar_position: 1
---

# Scaffolding a new project

## About `AELF Contract Templates`

Streamlined framework for swift and secure smart contract development on AElf blockchain. Eliminates template code, enforces best practices, and ensures modularity and interoperability.

## 1. Install

To install `AELF Contract Templates`, run the following command at the Terminal:

```bash
dotnet new install AElf.ContractTemplates
```

`dotnet new aelf` is now available in your terminal.

## 2. Help

To view more information, you can run the command `dotnet new aelf --help`:

```bash
dotnet new aelf --help
# AElf Contract (C#)
# Author: AElf

# Usage:
#   dotnet new aelf [options] [template options]

# Options:
#   -n, --name <name>       The name for the output being created. If no name is
#                           specified, the name of the output directory is used.
#   -o, --output <output>   Location to place the generated output.
#   --dry-run               Displays a summary of what would happen if the given
#                           command line were run if it would result in a
#                           template creation.
#   --force                 Forces content to be generated even if it would
#                           change existing files.
#   --no-update-check       Disables checking for the template package updates
#                           when instantiating a template.
#   --project <project>     The project that should be used for context
#                           evaluation.
#   -lang, --language <C#>  Specifies the template language to instantiate.
#   --type <project>        Specifies the template type to instantiate.

# Template options:
#   -N, --NamespacePath <NamespacePath>  Type: string
#                                        Default: AElf.Contracts.HelloWorld
```
