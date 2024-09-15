<script lang="ts">
	import { settings } from '$settings';
	let max_cols = $state(12);
	let gutter_size = $state(1);
</script>

<main class="layout" style:--gcs={max_cols}>
	<div class="full sub">
		<h1 class="content">{settings.app_name}</h1>

		<div class="content">
			<label for="max_cols">Max Columns</label>
			<input id="max_cols" type="number" bind:value={max_cols} step="4" />
		</div>

		<div class="layout full" style:--gcs={max_cols}>
			<div class="col c-half"><p>.c-half</p></div>
			<div class="col c-half"><p>.c-half</p></div>
			<div class="col c-full"><p>.c-full</p></div>
			<div class="col c-quarter"><p>.c-quarter</p></div>
			<div class="col c-quarter"><p>.c-quarter</p></div>
			<div class="col c-quarter"><p>.c-quarter</p></div>
			<div class="col c-quarter"><p>.c-quarter</p></div>

			<div class="col" style="--start: 1; --span: 1;"><p>--start: 1;<br />--span: 1;</p></div>
			<div class="col" style="--start: 2; --span: 1;"><p>--start: 2;<br />--span: 1;</p></div>
			<div class="col" style="--start: 3; --span: 1;"><p>--start: 3;<br />--span: 1;</p></div>
			<div class="col" style="--start: 4; --span: 1;"><p>--start: 4;<br />--span: 1;</p></div>
			<div class="col" style="--start: 5; --span: 1;"><p>--start: 5;<br />--span: 1;</p></div>
			<div class="col" style="--start: 6; --span: 1;"><p>--start: 6;<br />--span: 1;</p></div>
			<div class="col" style="--start: 7; --span: 1;"><p>--start: 7;<br />--span: 1;</p></div>
			<div class="col" style="--start: 8; --span: 1;"><p>--start: 8;<br />--span: 1;</p></div>
			<div class="col" style="--start: 9; --span: 1;"><p>--start: 9;<br />--span: 1;</p></div>
			<div class="col" style="--start: 10; --span: 1;"><p>--start: 10;<br />--span: 1;</p></div>
			<div class="col" style="--start: 11; --span: 1;"><p>--start: 11;<br />--span: 1;</p></div>
			<div class="col" style="--start: 12; --span: 1;"><p>--start: 12;<br />--span: 1;</p></div>
		</div>
	</div>
</main>

<style>
	.layout {
		gap: 20px 0;
	}

	.layout {
		display: grid;
		align-items: start;
		--gcs: 12;
		--gg: 2.5;
		--gc: minmax(50px, 100px);
		--g-boundary: minmax(calc(var(--gg) * 1%), 1fr);
		--g-gutter-width: calc(var(--gg) * 1%);

		grid-template-columns:
			[start gutter] var(--g-boundary) [content]
			repeat(calc(var(--gcs) - 1), [col-start] var(--gc) [col-end gutter] var(--g-gutter-width))
			[last-col-start col-start] var(--gc) [col-end content-end gutter] var(--g-boundary)
			[end];
		@media (width < 1000px) {
			--gcs: 8 !important;
		}
		@media (width < 500px) {
			--gcs: 4 !important;
		}
	}

	.layout > * {
		grid-column: col-start round(down, mod(calc(var(--start) - 1), var(--gcs)) + 1) / span
			var(--span, 'end');
	}

	.col {
		border: 1px solid var(--fg);
		height: 100px;
		align-items: center;
		display: flex;
		justify-content: center;
		box-shadow: 0 2px 10px 1px rgb(0 0 0 / 0.2);
		p {
			--fl: -2;
			margin: 0;
			text-align: center;
		}
	}

	.c-quarter {
		--start: 1; /* Always starts at column 2 */
		--span: calc((var(--gcs) / 2) - 1); /* Half of the total columns, excluding the first gutter */
	}

	.c-quarter:nth-child(2 of .c-quarter) {
		--start: calc((var(--gcs) / 4) + 1);
	}

	.c-quarter:nth-child(3 of .c-quarter) {
		--start: calc((var(--gcs) / 4) * 2 + 1);
	}

	.c-quarter:nth-child(4 of .c-quarter) {
		--start: calc(((var(--gcs) / 4) * 3) + 1);
	}

	.c-half {
		--start: 1;
		--span: calc((var(--gcs) - 1)); /* Half of the total columns, excluding the first gutter */
		& + .c-half {
			--start: calc(
				(var(--gcs) / 2) + 1
			); /* Starts after the first .c-half including its span and the gutter */
		}
	}

	.c-full {
		--start: 1;
		--span: calc((var(--gcs) * 2 - 1));
	}
</style>
