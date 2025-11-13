<script lang="ts">
	let { children } = $props();
</script>

<nav style="margin-bottom:2rem;">
  <a href="/">home</a> |
  <a href="/ninja">ninja</a> |
  <a href="/slots">slots</a>
</nav>
{@render children()}
