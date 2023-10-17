This is a repo for testing markdown and other doc stuff.

CORS demo:

- [No CORS error](https://crandmck.github.io/test-md/iframe-no-cors.html#something) - The URL is <code>https://crandmck.github.io/test-md/iframe-no-cors.html#something</code> and the iframe is on this domain.  Notice it scrolls down to the anchor for "Something".
- [CORS error](https://crandmck.github.io/test-md/iframe-with-cors-error.html#manifest-assertion) - The URL is <code>https://crandmck.github.io/test-md/iframe-with-cors-error.html#manifestassertion)</code> but the iframe is to <code>https://contentauth.github.io/json-manifest-reference/reference-cai</code> which is a different domain.  Doesn't scroll and you'll see CORS error in console.
