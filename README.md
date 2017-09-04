# Golua Unicode Support

This extension to [Arzilli's Golua](http://github.com/aarzilli/golua) adds
Unicode support to all functions from the Lua string library.

Lua patterns are replaced by
[Go regexps](http://github.com/google/re2/wiki/Syntax). This breaks
compatibility with Lua, but Unicode support breaks it anyways and Go regexps are
more powerful.

## Example

``` go
package main

import (
	"github.com/ambrevar/golua/unicode"
	"github.com/aarzilli/golua/lua"
)

func main() {
	L := lua.NewState()
	defer L.Close()
	L.OpenLibs()
	unicode.GoLuaReplaceFuncs(L)

	L.DoString(`print(string.len("résumé"))`)
	L.DoString(`print(string.upper("résumé"))`)
	L.DoString(`print(string.gsub("résumé", "\\pL", "[$0]"))`)
}
```
