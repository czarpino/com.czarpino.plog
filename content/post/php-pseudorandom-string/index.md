---
title: "PHP Pseudo Random String"
description: "Programmers not mind readers"
date: "2018-09-18"
tags: ["project management"]
---

When writing a random string generator in PHP, you must first consider whether or not you need a generator for a throwaway string ( e.g. placeholder or sample username) or a sensitive data (like a default password, application token, or salt). If you are generating for the latter, this article is for you.

### Arbitrary length strings

Generating a random string in PHP involves two main steps:

1. First is generating a cryptographically secure set of random bytes
2. and second is encoding the bytes into a string of printable characters

For generating random bytes, there are two main approaches depending on PHP version. The pre-PHP7 approach uses [`openssl_random_pseudo_bytes`](http://php.net/manual/en/function.openssl-random-pseudo-bytes.php) while the PHP7 approach prefers [`random_bytes`](http://php.net/manual/en/function.random-bytes.php). An advantage of the latter is that it is native and does not need additional modules installed. If needed, `openssl_random_pseudo_bytes` is still available in PHP7 as an extension. But as both functions are considered cryptographically secure generators anyway, `random_bytes` is the recommended function.

For encoding the bytes into printable characters, there are also a couple of viable approaches. Most popular of these are [`base64_encode`](http://php.net/manual/en/function.base64-encode.php) and [`bin2hex`](http://php.net/manual/en/function.bin2hex.php). You generally can't go wrong with either of these although `bin2hex` does have the advantage of being more predictable in length while `base64_encode` produces a shorter string with more variety in characters used.

Concretely, here is how you can generate a cryptographically secure random string :

```php
// Pre PHP7
$numOfBytes = 10;
$randomBytes = openssl_random_pseudo_bytes($numOfBytes);
$randomString = base64_encode($randomBytes);

/// PHP7+
$numOfBytes = 10;
$randomBytes = random_bytes($numOfBytes);
$randomString = base64_encode($randomBytes);
```

If you need some predictability such as generating string with a specific length, encoding bytes using `bin2hex` will be more suitable despite being limited to even length strings only.

```php
// Need to generate string with length 20!

// First generate 10 random bytes
$randomBytes = random_bytes(10);

// Now encode to get a 20 character string
$randomString = bin2hex($randomBytes);
```

#### Exact length strings

If you want complete control on the length of the random string generated, it would be more suitable to use PHP7's `random_int` function. And if your system is on PHP5, you can use a polyfill library called [`random_compat`](https://github.com/paragonie/random_compat).

```php
// Generate a 20 character string
$randomStr = '';
$allowedCharacters='0123456789abcdef';
for (
    $i = 0, $allowedMaxIdx = mb_strlen($allowedCharacters) - 1;
    $i < 20;
    $i ++
) {
    $randomStr .= $allowedCharacters[random_int(0, $allowedMaxIdx)];
}
```

And that's how you generate secure random strings in PHP. Happy coding!
