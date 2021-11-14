<h1 align="center">
  <img src="https://dslv9ilpbe7p1.cloudfront.net/Cj7cYvaXaoyQ386pQ2yIjw_store_logo_image.png" width="80"/><br/>
  Stockdroid Fans
</h1>
<h2 align="center">
  <img src="https://camo.githubusercontent.com/de4fa40cddcfcb22448cdca8e9dad69d8133ae62964a9c90ffa661afd780b94a/68747470733a2f2f656d6f6a6970656469612d75732e73332e6475616c737461636b2e75732d776573742d312e616d617a6f6e6177732e636f6d2f7468756d62732f3332302f6170706c652f3238352f706f6c6963652d6361722d6c696768745f31663661382e706e67" width="20"/>
  .h CRASH TEST
</h2>
<h3 align="center">
  Null character exploit
</h3>
<div id="deprecated" align="center">

  **Outdated**. This was created for archival
purposes only (and because i had nothing better to do).

</div>

You might be familiar with how string encoding and
particularly URL encoding work. You might also know
that, in order to define the bytes in memory that
the computer should read to parse the string, there
exists a **null character** (`\0`) that marks the
end of a string.

In C, this is the equivalent of doing:
```c
char *str = malloc(17);

str[0] = 'O'; str[1] = 'w'; str[2] = 'O';
str[3] = ' '; str[4] = 'w'; str[5] = 'h';
str[6] = 'a'; str[7] = 't'; str[8] = "'";
str[9] = 's'; str[10] = ' '; str[11] = 't';
str[11] = 'h'; str[12] = 'i'; str[13] = 's';
str[14] = '~'; str[15] = '?';

str[16] = '\0';

free(str)

// or simply

char str[] = 'OwO what's this~?'
```
In both cases, this will return '`OwO what's this~?`'.

URL encoding works in a similar fashion. To store
special characters in a URI string, the `%` character
is used (giving it the more popular name of 'percent
encoding').

Likewise, doing the following in a URI:
```js
"https://api.telegram.org/bot/sendMessage?chat_id=@stockdroidfans&text=Hello%20world!%20Press%20%2Fstart!"
```
…will return:
```jsonc
"ok": true,
"result" {
  // …,
  text = "Hello world! Press /start!"
}
```

You may see what's next coming. Since we can encode
virtually any character in UTF-8 and beyond using
URI encoding, doing this:
```js
"http://x/%%30%30"
```
Will return:
```js
"http://x/%00"
```

`%00` is a null character.

In most Chromium–based browsers, that means a crash,
since having two null characters in a string is
invalid.

Try it!

<h2 align="center">

  [http://x/%%30%30](http://x/%%30%30)

</h2>
