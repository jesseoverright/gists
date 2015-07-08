# Regex Gists

### Match exact string 

Uses start of line (^) and end of line ($)

    ^searchvalue$

## Pattern Matching

### One or more ASCII characters

    [a-zA-Z0-9]+

or zero or more

    [a-zA-Z0-9]*

### 3 to 5 numbers

    [0-9]{3,5}

### Negative regex (no numbers)

    [^0-9]

## Placeholders

    ^/name/([a-zA-Z]+)/$ index.php?name=$1

## Examples

### Phone Number

    [2-9][0-9]{2}-[0-9]{4}

### Most Email Addresses

    ^[a-zA-Z0-9_-.+]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$



## URL Routing Gists
