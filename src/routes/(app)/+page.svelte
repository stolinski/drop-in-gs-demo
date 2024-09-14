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
			<div class="col c-half"></div>
			<div class="col c-half"></div>
			<div class="col c-full"></div>
			<div class="col c-quarter"></div>
			<div class="col c-quarter"></div>
			<div class="col c-quarter"></div>
			<div class="col c-quarter"></div>

			<div class="col" style="--start: 1; --span: 1;"></div>
			<div class="col" style="--start: 2; --span: 1;"></div>
			<div class="col" style="--start: 3; --span: 1;"></div>
			<div class="col" style="--start: 4; --span: 1;"></div>
			<div class="col" style="--start: 5; --span: 1;"></div>
			<div class="col" style="--start: 6; --span: 1;"></div>
			<div class="col" style="--start: 7; --span: 1;"></div>
			<div class="col" style="--start: 8; --span: 1;"></div>
			<div class="col" style="--start: 9; --span: 1;"></div>
			<div class="col" style="--start: 10; --span: 1;"></div>
			<div class="col" style="--start: 11; --span: 1;"></div>
			<div class="col" style="--start: 12; --span: 1;"></div>
		</div>
	</div>
</main>

<style>
	.layout {
		display: grid;
		grid-template-rows: auto;
		grid-auto-flow: dense;
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
	}

	.layout > * {
		grid-column: col-start round(down, mod(calc(var(--start) - 1), var(--gcs)) + 1) / span
			var(--span, 'end');
	}

	.col {
		border: 1px solid #000;
		height: 100px;
		box-shadow: 0 2px 10px 1px rgb(0 0 0 / 0.2);
	}

	.c-quarter {
		--start: 1; /* Always starts at column 2 */
		--span: calc((var(--gcs) / 2) - 1); /* Half of the total columns, excluding the first gutter */
		& + .c-quarter {
			--start: calc((var(--gcs) / 4) + 1);
			& + .c-quarter {
				--start: calc((var(--gcs) / 4) * 2 + 1);
				& + .c-quarter {
					--start: calc(((var(--gcs) / 4) * 3) + 1);
				}
			}
		}
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
