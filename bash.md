# Other bash

## Default Arguments

```bash
#!/usr/bin/env bash
main () {
    local name=${1:-"you"}
    printf "One for %s, one for me.\n" "$name"
    return 0
}
main "$@"
```

## Split String

Don't quote and override IFS

```bash
IFS=" -_*"
for word in $1; do
    acronym+="${word:0:1}"
done
```

## Join String

Overwrite IFS with the desired delimiter and use [*]

FIND EXAMPLE

## Match Regex

```bash
[[$1 =~ ^[0-9]+$]]
```

Character classes

```bash
[[ ! $char =~ [[:digit:]] ]]
[[:alnum:]]
```

Capture Groups

```bash
if [[ $line =~ ^(.+)__(.*) ]]; then
    post=${BASH_REMATCH[2]}
    pre=${BASH_REMATCH[1]}
    if [[ $pre =~ ^(.*)__(.+) ]]; then
    printf -v __process_strong_line "%s<strong>%s</strong>%s" "${BASH_REMATCH[1]}" "${BASH_REMATCH[2]}" "$post"
    fi
fi
```

## Range

Can only be literal values

```bash
{a..z}
```

## Function resolves to exit status of last statement

```bash
is_silent() {
	validate_parameter_count 1 "$@"
	local -r sentence="$1"
	[[ -z ${sentence//[[:space:]]/} ]]
}
```

## Case

```bash
case "$letter" in
    A | E | I | O | U | L | N | R | S | T)
        __score=1
        ;;
    D | G)
        __score=2
        ;;
    B | C | M | P)
        __score=3
        ;;
    F | H | V | W | Y)
        __score=4
        ;;
    K)
        __score=5
        ;;
    J | X)
        __score=8
        ;;
    Q | Z)
        __score=10
        ;;
    *)
        return 1
        ;;
esac
```

## Name refs

Closest thing to reference.
Allows a callee to modify local state from a caller

## Random Number

`$RANDOM`

## Globing

TODO

## File System

```bash
readarray -t primes < ./primes.txt
```

```bash
IFS=$' ,'
read -r -a words <<< "$(echo -e "$1" | tr -d '\n')"
```

---