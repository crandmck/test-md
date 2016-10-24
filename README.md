# test-md
For testing markdown stuff

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
| `PATCH`&nbsp;`/MyModels/:id` | `prototype.updateAttributes` | `prototype.updateAttributes` |
