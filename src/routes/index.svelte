<script>
  import { page } from "$app/stores";

  console.log($page.url.pathname);
</script>

<h1>{$page.url.pathname}</h1>
