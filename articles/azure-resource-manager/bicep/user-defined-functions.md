---
title: User-defined functions in Bicep
description: Describes how to define and use user-defined functions in Bicep.
ms.topic: conceptual
ms.custom: devx-track-bicep
ms.date: 03/15/2024
---

# User-defined functions in Bicep

Within your Bicep file, you can create your own functions. These functions are available for use in your Bicep files. User-defined functions are separate from the [standard Bicep functions](./bicep-functions.md) that are automatically available within your Bicep files. Create your own functions when you have complicated expressions that are used repeatedly in your Bicep files.

[Bicep CLI version 0.26.X or higher](./install.md) is required to use this feature.

## Limitations

There are some restrictions when defining a user function:

* The function can't access variables.
* The function can only use parameters that are defined in the function.
* The function can't use the [reference](bicep-functions-resource.md#reference) function or any of the [list](bicep-functions-resource.md#list) functions.
* Parameters for the function can't have default values.

## Define functions

Use the `func` statement to define user-defined functions.

```bicep
@<decorator>(<argument>)
func <user-defined-function-name> (<argument-name> <data-type>, <argument-name> <data-type>, ...) <function-data-type> => <expression>
```

## Examples

The following examples show how to define and use user-defined functions:

```bicep
func buildUrl(https bool, hostname string, path string) string => '${https ? 'https' : 'http'}://${hostname}${empty(path) ? '' : '/${path}'}'

func sayHelloString(name string) string => 'Hi ${name}!'

func sayHelloObject(name string) object => {
  hello: 'Hi ${name}!'
}

func nameArray(name string) array => [
  name
]

func addNameArray(name string) array => [
  'Mary'
  'Bob'
  name
]

output azureUrl string = buildUrl(true, 'microsoft.com', 'azure')
output greetingArray array = map(['Evie', 'Casper'], name => sayHelloString(name))
output greetingObject object = sayHelloObject('John')
output nameArray array = nameArray('John')
output addNameArray array = addNameArray('John')

```

The outputs from the preceding examples are:

| Name | Type | Value |
| ---- | ---- | ----- |
| azureUrl | String | https://microsoft.com/azure |
| greetingArray | Array | ["Hi Evie!","Hi Casper!"] |
| greetingObject | Object | {"hello":"Hi John!"} |
| nameArray | Array | ["John"] |
| addNameArray | Array | ["Mary","Bob","John"] |

With [Bicep CLI version 0.23.X or higher](./install.md), you have the flexibility to invoke another user-defined function within a user-defined function. In the preceding example, with the function definition of `sayHelloString`, you can redefine the `sayHelloObject` function as:

```bicep
func sayHelloObject(name string) object => {
  hello: sayHelloString(name)
}
```

User-defined functions support using [user-defined data types](./user-defined-data-types.md).  For example:

```bicep
@minValue(0)
type positiveInt = int

func typedArg(input string[]) positiveInt => length(input)

param inArray array = [
  'Bicep'
  'ARM'
  'Terraform'
]

output elements positiveInt = typedArg(inArray)
```

The output from the preceding example is:

| Name | Type | Value |
| ---- | ---- | ----- |
| elements | positiveInt | 3 |

## Use decorators

Decorators are written in the format `@expression` and are placed above function declarations. The following table shows the available decorators for functions.

| Decorator | Argument | Description |
| --------- | ----------- | ------- |
| [description](#description) | string | Provide descriptions for the function. |
| [export](#export) | none | Indicates that the function is available for import by another Bicep file. |

Decorators are in the [sys namespace](bicep-functions.md#namespaces-for-functions). If you need to differentiate a decorator from another item with the same name, preface the decorator with `sys`. For example, if your Bicep file includes a variable named `description`, you must add the sys namespace when using the **description** decorator.

### Description

To add explanation, add a description to function declaration. For example:

```bicep
@description('The say hello function.')
func sayHelloString(name string) string => 'Hi ${name}!'
```

Markdown-formatted text can be used for the description text.

### Export

Use `@export()` to share the function with other Bicep files. For more information, see [Export variables, types, and functions](./bicep-import.md#export-variables-types-and-functions).

## Next steps

* To learn about the Bicep file structure and syntax, see [Understand the structure and syntax of Bicep files](./file.md).
* For a list of the available Bicep functions, see [Bicep functions](./bicep-functions.md).
