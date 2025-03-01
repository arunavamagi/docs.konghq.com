---
#
#  WARNING: this file was auto-generated by a script.
#  DO NOT edit this file directly. Instead, send a pull request to change
#  https://github.com/Kong/kong/tree/master/autodoc/pdk/ldoc/ldoc.ltp
#  or its associated files
#
title: kong.vault
pdk: true
toc: true
---

This module can be used to resolve, parse, and verify vault references.


## kong.vault.is_reference(reference)

Checks if the passed in reference looks like a reference.
 Valid references start with `{vault://` and end with `}`.

 If you need more thorough validation,
 use `kong.vault.parse_reference`.


**Parameters**

* **reference** (`string`):   reference to check

**Returns**

* `boolean`:  `true` is the passed in reference looks like a reference, otherwise `false`


**Usage**

``` lua
kong.vault.is_reference("{vault://env/key}") -- true
kong.vault.is_reference("not a reference")   -- false
```



## kong.vault.parse_reference(reference)

Parses and decodes the passed in reference and returns a table
 containing its components.

 Given a following resource:
 ```lua
 "{vault://env/cert/key?prefix=SSL_#1}"
 ```

 This function will return following table:

 ```lua
 {
   name     = "env",  -- name of the Vault entity or Vault strategy
   resource = "cert", -- resource where secret is stored
   key      = "key",  -- key to lookup if the resource is secret object
   config   = {       -- if there are any config options specified
     prefix = "SSL_"
   },
   version  = 1       -- if the version is specified
 }
 ```


**Parameters**

* **reference** (`string`):   reference to parse

**Returns**

1.  `table|nil`:  a table containing each component of the reference, or `nil` on error

1.  `string|nil`:  error message on failure, otherwise `nil`


**Usage**

``` lua
local ref, err = kong.vault.parse_reference("{vault://env/cert/key?prefix=SSL_#1}") -- table
```



## kong.vault.get(reference)

Resolves the passed in reference and returns the value of it.

**Parameters**

* **reference** (`string`):   reference to resolve

**Returns**

1.  `string|nil`:  resolved value of the reference

1.  `string|nil`:  error message on failure, otherwise `nil`


**Usage**

``` lua
local value, err = kong.vault.get("{vault://env/cert/key}")
```
