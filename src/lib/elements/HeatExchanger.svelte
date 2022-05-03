<script lang='ts'>
	export let x: number;
	export let y: number;

	export let namePosition: 'right' | 'left' = 'right';

	export let name = '';
</script>


{#if namePosition === 'right'}
	<svg x={x} y={y} width='122' height='76' viewBox='0 0 122 76' fill='none' xmlns='http://www.w3.org/2000/svg'>
		<rect x='37.7089' y='0.707107' width='52.2389' height='52.2389' transform='rotate(45 37.7089 0.707107)'
					stroke='red' />
		<line x1='37.8539' y1='0.733284' x2='37.8539' y2='74.5579' stroke='black' />
		<path
			d='M74.6212 37.6456L69.6212 34.7588V40.5323L74.6212 37.6456ZM0.796658 37.6456L5.79666 40.5323V34.7588L0.796658 37.6456ZM70.1212 37.1456H5.29666V38.1456H70.1212V37.1456Z'
			fill='black' />
		<text fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='12'
					letter-spacing='0em'>
            <tspan x='49.3379' y='9.86364'>{name}</tspan>
    </text>
	</svg>

{:else}
	<svg width='136' height='76' viewBox='0 0 136 76' fill='none' x={x - 60} y={y} xmlns='http://www.w3.org/2000/svg'>
		<rect x='97.6456' y='0.707107' width='52.2389' height='52.2389' transform='rotate(45 97.6456 0.707107)'
					stroke='black' />
		<line x1='97.7906' y1='0.733284' x2='97.7906' y2='74.5579' stroke='black' />
		<path
			d='M134.558 37.6456L129.558 34.7588V40.5323L134.558 37.6456ZM60.7334 37.6456L65.7334 40.5323V34.7588L60.7334 37.6456ZM130.058 37.1456H65.2334V38.1456H130.058V37.1456Z'
			fill='black' />
		<text fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='12'
					letter-spacing='0em'><tspan x='0.337891' y='15.8636'>{name}</tspan></text>
	</svg>
{/if}
