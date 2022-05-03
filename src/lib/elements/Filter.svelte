<script lang='ts'>
	export let x = 0;
	export let y = 0;

	export let name = '';
</script>


<svg width='108' height='76' viewBox='0 0 108 76' fill='none' x={x - 69} {y} xmlns='http://www.w3.org/2000/svg'>
	<rect x='69.6455' y='0.707107' width='52.2389' height='52.2389' transform='rotate(45 69.6455 0.707107)'
				stroke='green' />
	<path d='M33 38L106 38' stroke='black' stroke-dasharray='4 4' />
	<text fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='12'
				letter-spacing='0em'><tspan x='0' y='11.8636'>{name}</tspan></text>
</svg>
