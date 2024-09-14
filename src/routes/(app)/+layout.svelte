<script lang="ts">
	import Footer from '$routes/(app)/Footer.svelte';

	let { children } = $props()

</script>

{@render children()}


<Footer />
