# Regex Gists

### Start of line (^)

    ^first

### End of line ($)

    end$

### Placeholders

    ^/name/([a-zA-Z]+)/$ index.php?name=$1

## Examples

### One ore more ASCII characters

    [a-zA-Z0-9]+
    # or zero or more
    [a-zA-Z0-9]*

### 3 to 5 numbers

    [0-9]{3,5}

### Phone Number

    [2-9][0-9]{2}-[0-9]{4}

### Most Email Addresses

    ^[a-zA-Z0-9_-.+]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$

### Negative regex (no numbers)

    [^0-9]

## URL Routing Gists
