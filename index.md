# Welcome to the configng wiki!
## Under heavy testing and development
 many thing will change this is a basic idea of how setup a function group
## Coding standards

```
# @description Strip characters from the beginning of a string.
#
# @example
#   echo "$(string::lstrip "Hello World!" "He")"
#   #Output
#   llo World!
#
# @arg $1 string The input string.
# @arg $2 string The characters you want to strip.
#
# @exitcode 0  If successful.
# @exitcode 2 Function missing arguments.
#
# @stdout Returns the modified string.
string::lstrip() {
[[ $# -lt 2 ]] && printf "%s: Missing arguments\n" "${FUNCNAME[0]}" && return 2
printf '%s\n' "${1##$2}"
}
```

Functions should follow ~~filename~~::func_name style. Then you can tell just from the name which 
file the function is located in. Return codes should also follow a similar pattern:
* 0 Successful
* 1 Not found
* 2 Function missing arguments
* 3-255 all other errors

Validate values:
```
# Validate minimum frequency is <= maximum frequency
[ "$min_freq" -gt "$max_freq" ] && printf "%s: Minimum frequency must be <= maximum frequency\n" "${FUNCNAME[0]}" && return 5
```

Return values should use stdout:
```
# Return value
printf '%s\n' "$(cat $file)"
```

Only use sudo when needed and never run as root!
