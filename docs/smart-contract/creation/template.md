---
sidebar_position: 1
---

# Scaffolding a new project

The `AELF Contract Templates` (AElf.ContractTemplates) tool provides a streamlined foundation for developing smart contracts on the aelf blockchain platform. This tool offers a standardized and efficient starting point, accelerating the development process by eliminating boilerplate code and promoting best practices. Developers can leverage `AELF Contract Templates` to create secure, modular, and interoperable smart contracts within the aelf ecosystem.

# Install

To install `AELF Contract Templates`, run the following command at the Terminal:

```bash
dotnet new install AElf.ContractTemplates
```

`dotnet new aelf` is now available in your terminal.

# Help

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
