# sveltekit-page.url.pathname

Minimal repro of a `$page.url.pathname` bug when building a SvelteKit app using the static adapter.

**UPDATE**: This bug was partially fixed in [@sveltejs/kit version 1.0.0-next.213](https://github.com/sveltejs/kit/blob/6c9b73977f7cb54902c55ccc395510b7ac3eb35b/packages/kit/CHANGELOG.md#100-next213).

## Repro steps

### 1) Run `yarn dev`

`$page.url.pathname` should display a forward slash (`/`).

### 1) Run `yarn build`

Build the app using the static adapter.

Serve the `build` folder:

```sh
serve build
```

`$page.url.pathname` displays `//prerender/`.

When inspecting `build/index.html`, `hydrate.url` is set to `new URL("sveltekit://prerender/")`.

```html
<!-- build/index.html -->
<script type="module">
  import { start } from "/_app/start-90034bf0.js";
  start({
    target: document.querySelector("#svelte"),
    paths: { base: "", assets: "" },
    session: {},
    route: true,
    spa: false,
    trailing_slash: "never",
    hydrate: {
      status: 200,
      error: null,
      nodes: [
        import("/_app/layout.svelte-96b29dd0.js"),
        import("/_app/pages/index.svelte-9bf7f989.js"),
      ],
      url: new URL("sveltekit://prerender/"),
      params: {},
    },
  });
</script>
```
