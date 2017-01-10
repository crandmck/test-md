# test-md
For testing markdown stuff.

{% include note.html content="In addition to these properties, you can use additional parameters supported by [`node-mysql`](https://github.com/felixge/node-mysql).
" %}

Something interesting here.

<div class="gh-only">
<p>This is some stuff that won't be displayed in the docs.
You have to use HTML inside this block, not markdown, e.g. 
<a href="http://loopback.io/docs">LoopBack docs</a>.</p>
</div>

| HTTP endpoint | 3.x method | 2.x method |
|---|---|---|
| `PUT`&nbsp;`/MyModels` | `replaceOrCreate` | `updateOrCreate` |
| `PUT`&nbsp;`/MyModels/:id` | `replaceById` | `prototype.updateAttributes` |
| `PATCH`&nbsp;`/MyModels` | `updateOrCreate` | `updateOrCreate` |
| <a name="patch1"></a>`PATCH`&nbsp;`/MyModels/:id` | `prototype.updateAttributes` | `prototype.updateAttributes` |

## Table demo

Typical table in a README:

| Option | Type | Default | Description |
| ---- | ---- | ---- | ---- |
| debug | Boolean&nbsp;&nbsp;&nbsp; | `false` | If `true`, HTTP responses include all error properties, including sensitive data such as file paths, URLs and stack traces. See [Example output](#example) below. |
| log | Boolean | `true` |  If `true`, all errors are printed via `console.error`, including an array of fields (custom error properties) that are safe to include in response messages (both 4xx and 5xx). <br/> If `false`, sends only the error back in the response. |

Same table restricted to 72 characters length:

123456789012345678901234567890123456789012345678901234567890123456789012

| Option | Type | Default | Description |
| ---- | ---- | ---- | ---- |
| debug | Boolean&nbsp;&nbsp;&nbsp; | `false` | If `true`, HTTP responses
include all error properties, including sensitive data such as file paths,
URLs and stack traces. See [Example output](#example) below. |
| log | Boolean | `true` |  If `true`, all errors are printed via 
`console.error`, including an array of fields (custom error properties)
that are safe to include in response messages (both 4xx and 5xx). 
<br/> If `false`, sends only the error back in the response. |


