# nim-strenc
This is a Nim library for automatic encryption (currently via XOR with a different key for each string generated at compile-time) of string literals.
You can install it from Nimble via
```sh
nimble install strenc
```
and then just use it like so:
```nim
import strenc
# After importing the module you don't have to do anything else to activate encryption
echo "hello world"
echo "how are you?"
```
In the compiled C code strings will look like this:
```c
STRING_LITERAL(TM__huvhZYSc4ExMXNTyiw83eQ_2, "!+# \"r$\?#:3", 11);
STRING_LITERAL(TM__huvhZYSc4ExMXNTyiw83eQ_3, "qul<|lz0h}f+", 12);
```
If you wish to disable all hints for places where the encryption was applied, add ``hint("Pattern", false)``
to your `.nims` config file, or, if you use `.cfg`, ``--hint[Pattern]:off``

### Please do not forget to strip your binaries if you want this library to be useful! Otherwise it'll be much easier to find the code which does string decryption.

## How does it work?
This library uses one of the lesser known Nim features - term-rewriting macros. They allow to implicitly *rewrite* code at compile-time by using different kinds of patterns. You can read more [in the manual here](https://nim-lang.org/docs/manual_experimental.html#term-rewriting-macros).

## Why?
Because it's fun and this library can actually help you to protect string data in the application from
not-so-experienced "haxxors".

### Do not forget that a person with enough programming and/or reverse-engineering knowledge will still be able to get the original content of all encrypted strings!