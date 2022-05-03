<script lang='ts'>
	import Tank from './elements/Tank.svelte';
	import HeatExchanger from './elements/HeatExchanger.svelte';
	import Filter from './elements/Filter.svelte';
</script>

<svg width='609' height='458' viewBox='0 0 609 458' fill='none' xmlns='http://www.w3.org/2000/svg'>
	<g id='circuit'>
		<Tank x='193.5' y='82.5' name='&#x420;&#x411; lll&#x43a;' />

		<Tank x='362.5' y='343.5' name='Банк СВЗ' namePosition='bottom' />

		<HeatExchanger x='278.709' y='102.707' name='TO lll-lV&#x43a; &#x2116;1' />

		<HeatExchanger x='278.709' y='289.707' name='TO lll-lV&#x43a; &#x2116;2' namePosition='left' />

		<Filter x={84.6455} y={322.707} name='&#x424;&#x418;&#x41e; lll&#x43a;' />

		<!--        <g id="filter">-->
		<!--            <rect id="Rectangle 2_3" x="84.6455" y="322.707" width="52.2389" height="52.2389" transform="rotate(45 84.6455 322.707)" stroke="black"/>-->
		<!--            <path id="Vector 3" d="M48 360L121 360" stroke="black" stroke-dasharray="4 4"/>-->
		<!--        </g>-->
		<g id='ovalve'>
			<path id='Polygon 1' d='M200.75 171.752L214.689 177.5L200.75 183.248L200.75 171.752Z' stroke='black' />
			<path id='Polygon 2' d='M228.25 171.752L214.311 177.5L228.25 183.248L228.25 171.752Z' stroke='black' />
			<rect id='Rectangle 3' x='206.5' y='159.5' width='15' height='7' stroke='black' />
			<line id='Line 1' x1='213.5' y1='178' x2='213.5' y2='166' stroke='black' />
			<line id='Line 2' x1='215.5' y1='178' x2='215.5' y2='166' stroke='black' />
		</g>
		<g id='ovalve_2'>
			<path id='Polygon 1_2' d='M310.752 405.25L316.5 391.311L322.248 405.25L310.752 405.25Z' stroke='black' />
			<path id='Polygon 2_2' d='M310.752 377.75L316.5 391.689L322.248 377.75L310.752 377.75Z' stroke='black' />
			<rect id='Rectangle 3_2' x='298.5' y='399.5' width='15' height='7' transform='rotate(-90 298.5 399.5)'
						stroke='black' />
			<line id='Line 1_2' x1='317' y1='392.5' x2='305' y2='392.5' stroke='black' />
			<line id='Line 2_2' x1='317' y1='390.5' x2='305' y2='390.5' stroke='black' />
		</g>
		<g id='ovalve_3'>
			<path id='Polygon 1_3' d='M310.752 275.25L316.5 261.311L322.248 275.25L310.752 275.25Z' stroke='black' />
			<path id='Polygon 2_3' d='M310.752 247.75L316.5 261.689L322.248 247.75L310.752 247.75Z' stroke='black' />
			<rect id='Rectangle 3_3' x='298.5' y='269.5' width='15' height='7' transform='rotate(-90 298.5 269.5)'
						stroke='black' />
			<line id='Line 1_3' x1='317' y1='262.5' x2='305' y2='262.5' stroke='black' />
			<line id='Line 2_3' x1='317' y1='260.5' x2='305' y2='260.5' stroke='black' />
		</g>
		<g id='ovalve_4'>
			<path id='Polygon 1_4' d='M310.752 220.25L316.5 206.311L322.248 220.25L310.752 220.25Z' stroke='black' />
			<path id='Polygon 2_4' d='M310.752 192.75L316.5 206.689L322.248 192.75L310.752 192.75Z' stroke='black' />
			<rect id='Rectangle 3_4' x='298.5' y='214.5' width='15' height='7' transform='rotate(-90 298.5 214.5)'
						stroke='black' />
			<line id='Line 1_4' x1='317' y1='207.5' x2='305' y2='207.5' stroke='black' />
			<line id='Line 2_4' x1='317' y1='205.5' x2='305' y2='205.5' stroke='black' />
		</g>
		<g id='ovalve_5'>
			<path id='Polygon 1_5' d='M310.752 89.25L316.5 75.3115L322.248 89.25L310.752 89.25Z' stroke='black' />
			<path id='Polygon 2_5' d='M310.752 61.75L316.5 75.6885L322.248 61.75L310.752 61.75Z' stroke='black' />
			<rect id='Rectangle 3_5' x='298.5' y='83.5' width='15' height='7' transform='rotate(-90 298.5 83.5)'
						stroke='black' />
			<line id='Line 1_5' x1='317' y1='76.5' x2='305' y2='76.5' stroke='black' />
			<line id='Line 2_5' x1='317' y1='74.5' x2='305' y2='74.5' stroke='black' />
		</g>
		<g id='ovalve_6'>
			<path id='Polygon 1_6' d='M121.75 301.752L135.689 307.5L121.75 313.248L121.75 301.752Z' stroke='black' />
			<path id='Polygon 2_6' d='M149.25 301.752L135.311 307.5L149.25 313.248L149.25 301.752Z' stroke='black' />
			<rect id='Rectangle 3_6' x='127.5' y='289.5' width='15' height='7' stroke='black' />
			<line id='Line 1_6' x1='134.5' y1='308' x2='134.5' y2='296' stroke='black' />
			<line id='Line 2_6' x1='136.5' y1='308' x2='136.5' y2='296' stroke='black' />
		</g>
		<g id='ovalve_7'>
			<path id='Polygon 1_7' d='M21.75 406.752L35.6885 412.5L21.75 418.248L21.75 406.752Z' stroke='black' />
			<path id='Polygon 2_7' d='M49.25 406.752L35.3115 412.5L49.25 418.248L49.25 406.752Z' stroke='black' />
			<rect id='Rectangle 3_7' x='27.5' y='394.5' width='15' height='7' stroke='black' />
			<line id='Line 1_7' x1='34.5' y1='413' x2='34.5' y2='401' stroke='black' />
			<line id='Line 2_7' x1='36.5' y1='413' x2='36.5' y2='401' stroke='black' />
		</g>
		<g id='cvalve'>
			<path id='Polygon 1_8' d='M34.25 127.499L46.377 132.5L34.25 137.501L34.25 127.499Z' fill='black' stroke='black'
						stroke-width='2' />
			<path id='Polygon 2_8' d='M60.75 127.499L48.623 132.5L60.75 137.501L60.75 127.499Z' fill='black' stroke='black'
						stroke-width='2' />
			<line id='Line 6' x1='41' y1='121.5' x2='54' y2='121.5' stroke='black' />
			<line id='Line 1_8' x1='46.5' y1='133' x2='46.5' y2='121' stroke='black' />
			<line id='Line 2_8' x1='48.5' y1='133' x2='48.5' y2='121' stroke='black' />
		</g>
		<g id='cvalve_2'>
			<path id='Polygon 1_9' d='M34.25 221.499L46.377 226.5L34.25 231.501L34.25 221.499Z' fill='black' stroke='black'
						stroke-width='2' />
			<path id='Polygon 2_9' d='M60.75 221.499L48.623 226.5L60.75 231.501L60.75 221.499Z' fill='black' stroke='black'
						stroke-width='2' />
			<line id='Line 6_2' x1='41' y1='215.5' x2='54' y2='215.5' stroke='black' />
			<line id='Line 1_9' x1='46.5' y1='227' x2='46.5' y2='215' stroke='black' />
			<line id='Line 2_9' x1='48.5' y1='227' x2='48.5' y2='215' stroke='black' />
		</g>
		<g id='cvalve_3'>
			<path id='Polygon 1_10' d='M34.25 220.499L46.377 225.5L34.25 230.501L34.25 220.499Z' fill='black' stroke='black'
						stroke-width='2' />
			<path id='Polygon 2_10' d='M60.75 220.499L48.623 225.5L60.75 230.501L60.75 220.499Z' fill='black' stroke='black'
						stroke-width='2' />
			<line id='Line 6_3' x1='41' y1='214.5' x2='54' y2='214.5' stroke='black' />
			<line id='Line 1_10' x1='46.5' y1='226' x2='46.5' y2='214' stroke='black' />
			<line id='Line 2_10' x1='48.5' y1='226' x2='48.5' y2='214' stroke='black' />
		</g>
		<g id='cn'>
			<circle id='Ellipse 1' cx='120' cy='39' r='24.5' stroke='black' />
			<path id='Arrow 2' d='M95 39L110 47.6603V30.3397L95 39Z' fill='black' />
		</g>
		<g id='cn_2'>
			<circle id='Ellipse 1_2' cx='120' cy='133' r='24.5' stroke='black' />
			<path id='Arrow 2_2' d='M95 133L110 141.66V124.34L95 133Z' fill='black' />
		</g>
		<g id='cn_3'>
			<circle id='Ellipse 1_3' cx='120' cy='227' r='24.5' stroke='black' />
			<path id='Arrow 2_3' d='M95 227L110 235.66V218.34L95 227Z' fill='black' />
		</g>
		<line id='Line 7' x1='95' y1='39' x2='61' y2='39' stroke='black' stroke-width='2' />
		<line id='Line 10' x1='95' y1='133' x2='61' y2='133' stroke='black' stroke-width='2' />
		<line id='Line 13' x1='95' y1='227' x2='61' y2='227' stroke='black' stroke-width='2' />
		<line id='Line 9' x1='317' y1='39' x2='144' y2='39' stroke='black' stroke-width='2' />
		<line id='Line 11' x1='174' y1='133' x2='144' y2='133' stroke='black' stroke-width='2' />
		<line id='Line 14' x1='174' y1='227' x2='144' y2='227' stroke='black' stroke-width='2' />
		<g id='mes'>
			<circle id='Ellipse 2' cx='214.5' cy='15.5' r='13' stroke='black' />
			<text id='C' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='208.907' y='20.5909'>C</tspan></text>
			<line id='Line 4' x1='212.5' y1='28' x2='212.5' y2='40' stroke='black' />
			<line id='Line 5' x1='216.5' y1='28' x2='216.5' y2='40' stroke='black' />
		</g>
		<g id='mes_2'>
			<circle id='Ellipse 2_2' cx='243.5' cy='58.5' r='13' stroke='black' />
			<text id='C_2' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='237.818' y='63.5909'>&#x41d;</tspan></text>
			<line id='Line 4_2' x1='241.5' y1='71' x2='241.5' y2='83' stroke='black' />
			<line id='Line 5_2' x1='245.5' y1='71' x2='245.5' y2='83' stroke='black' />
		</g>
		<g id='mes_3'>
			<circle id='Ellipse 2_3' cx='214.5' cy='401.5' r='13' stroke='black' />
			<text id='C_3' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='208.907' y='406.591'>C</tspan></text>
			<line id='Line 4_3' x1='212.5' y1='414' x2='212.5' y2='426' stroke='black' />
			<line id='Line 5_3' x1='216.5' y1='414' x2='216.5' y2='426' stroke='black' />
		</g>
		<g id='mes_4'>
			<circle id='Ellipse 2_4' cx='372.5' cy='208.5' r='13' stroke='black' />
			<text id='C_4' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='367.509' y='213.591'>T</tspan></text>
			<line id='Line 4_4' x1='370.5' y1='221' x2='370.5' y2='233' stroke='black' />
			<line id='Line 5_4' x1='374.5' y1='221' x2='374.5' y2='233' stroke='black' />
		</g>
		<g id='mes_5'>
			<circle id='Ellipse 2_5' cx='482.5' cy='287.5' r='13' stroke='black' />
			<text id='C_5' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='476.818' y='292.591'>H</tspan></text>
			<line id='Line 4_5' x1='480.5' y1='300' x2='480.5' y2='312' stroke='black' />
			<line id='Line 5_5' x1='484.5' y1='300' x2='484.5' y2='312' stroke='black' />
		</g>
		<g id='mes_6'>
			<circle id='Ellipse 2_6' cx='482.5' cy='123.5' r='13' stroke='black' />
			<text id='C_6' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='477.509' y='128.591'>T</tspan></text>
			<line id='Line 4_6' x1='480.5' y1='136' x2='480.5' y2='148' stroke='black' />
			<line id='Line 5_6' x1='484.5' y1='136' x2='484.5' y2='148' stroke='black' />
		</g>
		<g id='mes_7'>
			<circle id='Ellipse 2_7' cx='482.5' cy='15.5' r='13' stroke='black' />
			<text id='C_7' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='477.509' y='20.5909'>T</tspan></text>
			<line id='Line 4_7' x1='480.5' y1='28' x2='480.5' y2='40' stroke='black' />
			<line id='Line 5_7' x1='484.5' y1='28' x2='484.5' y2='40' stroke='black' />
		</g>
		<g id='mes_8'>
			<circle id='Ellipse 2_8' cx='584.5' cy='287.5' r='13' stroke='black' />
			<text id='C_8' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='578.818' y='292.591'>H</tspan></text>
			<line id='Line 4_8' x1='582.5' y1='300' x2='582.5' y2='312' stroke='black' />
			<line id='Line 5_8' x1='586.5' y1='300' x2='586.5' y2='312' stroke='black' />
		</g>
		<g id='mes_9'>
			<circle id='Ellipse 2_9' cx='584.5' cy='233.5' r='13' stroke='black' />
			<text id='C_9' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='578.668' y='238.591'>Q</tspan></text>
			<line id='Line 4_9' x1='582.5' y1='246' x2='582.5' y2='258' stroke='black' />
			<line id='Line 5_9' x1='586.5' y1='246' x2='586.5' y2='258' stroke='black' />
		</g>
		<g id='mes_10'>
			<circle id='Ellipse 2_10' cx='584.5' cy='69.5' r='13' stroke='black' />
			<text id='C_10' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='578.668' y='74.5909'>Q</tspan></text>
			<line id='Line 4_10' x1='582.5' y1='82' x2='582.5' y2='94' stroke='black' />
			<line id='Line 5_10' x1='586.5' y1='82' x2='586.5' y2='94' stroke='black' />
		</g>
		<g id='mes_11'>
			<circle id='Ellipse 2_11' cx='584.5' cy='123.5' r='13' stroke='black' />
			<text id='C_11' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='578.668' y='128.591'>Q</tspan></text>
			<line id='Line 4_11' x1='582.5' y1='136' x2='582.5' y2='148' stroke='black' />
			<line id='Line 5_11' x1='586.5' y1='136' x2='586.5' y2='148' stroke='black' />
		</g>
		<g id='mes_12'>
			<circle id='Ellipse 2_12' cx='584.5' cy='15.5' r='13' stroke='black' />
			<text id='C_12' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='578.668' y='20.5909'>Q</tspan></text>
			<line id='Line 4_12' x1='582.5' y1='28' x2='582.5' y2='40' stroke='black' />
			<line id='Line 5_12' x1='586.5' y1='28' x2='586.5' y2='40' stroke='black' />
		</g>
		<g id='mes2'>
			<circle id='Ellipse 2_13' cx='28.5' cy='275.5' r='13' transform='rotate(90 28.5 275.5)' stroke='black' />
			<text id='T' transform='translate(21.5 266.5)' fill='black' xml:space='preserve' style='white-space: pre'
						font-family='Inter' font-size='14' letter-spacing='0em'><tspan x='2.50879' y='13.5909'>T</tspan></text>
			<line id='Line 4_13' x1='16' y1='273.5' x2='2' y2='273.5' stroke='black' />
			<line id='Line 5_13' x1='16' y1='277.5' x2='2' y2='277.5' stroke='black' />
		</g>
		<g id='mes2_2'>
			<circle id='Ellipse 2_14' cx='120.5' cy='83.5' r='13' stroke='black' />
			<text id='&#206;&#148;P' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter'
						font-size='14' letter-spacing='0em'><tspan x='111.326' y='88.5909'>&#x394;P</tspan></text>
		</g>
		<g id='mes2_3'>
			<circle id='Ellipse 2_15' cx='120.5' cy='177.5' r='13' stroke='black' />
			<text id='&#206;&#148;P_2' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter'
						font-size='14' letter-spacing='0em'><tspan x='111.326' y='182.591'>&#x394;P</tspan></text>
		</g>
		<g id='mes2_4'>
			<circle id='Ellipse 2_16' cx='120.5' cy='271.5' r='13' stroke='black' />
			<text id='&#206;&#148;P_3' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter'
						font-size='14' letter-spacing='0em'><tspan x='111.326' y='276.591'>&#x394;P</tspan></text>
		</g>
		<path id='Vector 2' d='M107.5 84H85.5V38.5M133.5 84H155V40' stroke='black' />
		<path id='Vector 3_2' d='M107.5 178H85.5V132.5M133.5 178H155V134' stroke='black' />
		<path id='Vector 4' d='M107.5 272H85.5V226.5M133.5 272H155V228' stroke='black' />
		<g id='consumer'>
			<rect id='Rectangle 4' x='492.707' y='256.678' width='24' height='24' transform='rotate(-45 492.707 256.678)'
						stroke='black' />
			<line id='Line 16' x1='493' y1='256.5' x2='526' y2='256.5' stroke='black' />
			<path id='Vector 5'
						d='M510 257L512.887 252L507.113 252L510 257ZM509.5 240L509.5 252.5L510.5 252.5L510.5 240L509.5 240Z'
						fill='black' />
			<path id='Vector 6' d='M510 256L507.113 261H512.887L510 256ZM510.5 273V260.5H509.5V273H510.5Z' fill='black' />
			<text id='6' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='512.241' y='239.091'>5</tspan></text>
		</g>
		<g id='consumer_2'>
			<rect id='Rectangle 4_2' x='492.707' y='92.6777' width='24' height='24' transform='rotate(-45 492.707 92.6777)'
						stroke='black' />
			<line id='Line 16_2' x1='493' y1='92.5' x2='526' y2='92.5' stroke='black' />
			<path id='Vector 5_2' d='M510 93L512.887 88L507.113 88L510 93ZM509.5 76L509.5 88.5L510.5 88.5L510.5 76L509.5 76Z'
						fill='black' />
			<path id='Vector 6_2' d='M510 92L507.113 97H512.887L510 92ZM510.5 109V96.5H509.5V109H510.5Z' fill='black' />
			<text id='6_2' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='512.262' y='75.0909'>2</tspan></text>
		</g>
		<g id='consumer_3'>
			<rect id='Rectangle 4_3' x='492.707' y='202.678' width='24' height='24' transform='rotate(-45 492.707 202.678)'
						stroke='black' />
			<line id='Line 16_3' x1='493' y1='202.5' x2='526' y2='202.5' stroke='black' />
			<path id='Vector 5_3'
						d='M510 203L512.887 198L507.113 198L510 203ZM509.5 186L509.5 198.5L510.5 198.5L510.5 186L509.5 186Z'
						fill='black' />
			<path id='Vector 6_3' d='M510 202L507.113 207H512.887L510 202ZM510.5 219V206.5H509.5V219H510.5Z' fill='black' />
			<text id='6_3' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='512.009' y='185.091'>4</tspan></text>
		</g>
		<g id='consumer_4'>
			<rect id='Rectangle 4_4' x='492.707' y='38.6777' width='24' height='24' transform='rotate(-45 492.707 38.6777)'
						stroke='black' />
			<line id='Line 16_4' x1='493' y1='38.5' x2='526' y2='38.5' stroke='black' />
			<path id='Vector 5_4' d='M510 39L512.887 34L507.113 34L510 39ZM509.5 22L509.5 34.5L510.5 34.5L510.5 22L509.5 22Z'
						fill='black' />
			<path id='Vector 6_4' d='M510 38L507.113 43H512.887L510 38ZM510.5 55V42.5H509.5V55H510.5Z' fill='black' />
			<text id='6_4' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='513.246' y='21.0909'>1</tspan></text>
		</g>
		<g id='cvalve/closed'>
			<path id='Polygon 1_11' d='M537.75 304.752L551.689 310.5L537.75 316.248L537.75 304.752Z' stroke='black' />
			<path id='Polygon 2_11' d='M565.25 304.752L551.311 310.5L565.25 316.248L565.25 304.752Z' stroke='black' />
			<line id='Line 6_4' x1='545' y1='299.5' x2='558' y2='299.5' stroke='black' />
			<line id='Line 1_11' x1='550.5' y1='311' x2='550.5' y2='299' stroke='black' />
			<line id='Line 2_11' x1='552.5' y1='311' x2='552.5' y2='299' stroke='black' />
		</g>
		<g id='cvalve/closed_2'>
			<path id='Polygon 1_12' d='M537.75 250.752L551.689 256.5L537.75 262.248L537.75 250.752Z' stroke='black' />
			<path id='Polygon 2_12' d='M565.25 250.752L551.311 256.5L565.25 262.248L565.25 250.752Z' stroke='black' />
			<line id='Line 6_5' x1='545' y1='245.5' x2='558' y2='245.5' stroke='black' />
			<line id='Line 1_12' x1='550.5' y1='257' x2='550.5' y2='245' stroke='black' />
			<line id='Line 2_12' x1='552.5' y1='257' x2='552.5' y2='245' stroke='black' />
		</g>
		<g id='cvalve/closed_3'>
			<path id='Polygon 1_13' d='M537.75 86.7519L551.689 92.5L537.75 98.2481L537.75 86.7519Z' stroke='black' />
			<path id='Polygon 2_13' d='M565.25 86.7519L551.311 92.5L565.25 98.2481L565.25 86.7519Z' stroke='black' />
			<line id='Line 6_6' x1='545' y1='81.5' x2='558' y2='81.5' stroke='black' />
			<line id='Line 1_13' x1='550.5' y1='93' x2='550.5' y2='81' stroke='black' />
			<line id='Line 2_13' x1='552.5' y1='93' x2='552.5' y2='81' stroke='black' />
		</g>
		<g id='cvalve/closed_4'>
			<path id='Polygon 1_14' d='M537.75 140.752L551.689 146.5L537.75 152.248L537.75 140.752Z' stroke='black' />
			<path id='Polygon 2_14' d='M565.25 140.752L551.311 146.5L565.25 152.248L565.25 140.752Z' stroke='black' />
			<line id='Line 6_7' x1='545' y1='135.5' x2='558' y2='135.5' stroke='black' />
			<line id='Line 1_14' x1='550.5' y1='147' x2='550.5' y2='135' stroke='black' />
			<line id='Line 2_14' x1='552.5' y1='147' x2='552.5' y2='135' stroke='black' />
		</g>
		<g id='cvalve/closed_5'>
			<path id='Polygon 1_15' d='M537.75 32.7519L551.689 38.5L537.75 44.2481L537.75 32.7519Z' stroke='black' />
			<path id='Polygon 2_15' d='M565.25 32.7519L551.311 38.5L565.25 44.2481L565.25 32.7519Z' stroke='black' />
			<line id='Line 6_8' x1='545' y1='27.5' x2='558' y2='27.5' stroke='black' />
			<line id='Line 1_15' x1='550.5' y1='39' x2='550.5' y2='27' stroke='black' />
			<line id='Line 2_15' x1='552.5' y1='39' x2='552.5' y2='27' stroke='black' />
		</g>
		<g id='cvalve_4'>
			<g id='Property 1=Default'>
				<path id='Polygon 1_16' d='M34.25 33.4989L46.377 38.5L34.25 43.5011L34.25 33.4989Z' fill='black' stroke='black'
							stroke-width='2' />
				<path id='Polygon 2_16' d='M60.75 33.4989L48.623 38.5L60.75 43.5011L60.75 33.4989Z' fill='black' stroke='black'
							stroke-width='2' />
				<line id='Line 6_9' x1='41' y1='27.5' x2='54' y2='27.5' stroke='black' />
				<line id='Line 1_16' x1='46.5' y1='39' x2='46.5' y2='27' stroke='black' />
				<line id='Line 2_16' x1='48.5' y1='39' x2='48.5' y2='27' stroke='black' />
			</g>
		</g>
		<g id='cvalve/closed_6'>
			<path id='Polygon 1_17' d='M433.75 304.752L447.689 310.5L433.75 316.248L433.75 304.752Z' stroke='black' />
			<path id='Polygon 2_17' d='M461.25 304.752L447.311 310.5L461.25 316.248L461.25 304.752Z' stroke='black' />
			<line id='Line 6_10' x1='441' y1='299.5' x2='454' y2='299.5' stroke='black' />
			<line id='Line 1_17' x1='446.5' y1='311' x2='446.5' y2='299' stroke='black' />
			<line id='Line 2_17' x1='448.5' y1='311' x2='448.5' y2='299' stroke='black' />
		</g>
		<g id='cvalve/closed_7'>
			<path id='Polygon 1_18' d='M433.75 250.752L447.689 256.5L433.75 262.248L433.75 250.752Z' stroke='black' />
			<path id='Polygon 2_18' d='M461.25 250.752L447.311 256.5L461.25 262.248L461.25 250.752Z' stroke='black' />
			<line id='Line 6_11' x1='441' y1='245.5' x2='454' y2='245.5' stroke='black' />
			<line id='Line 1_18' x1='446.5' y1='257' x2='446.5' y2='245' stroke='black' />
			<line id='Line 2_18' x1='448.5' y1='257' x2='448.5' y2='245' stroke='black' />
		</g>
		<g id='cvalve/closed_8'>
			<path id='Polygon 1_19' d='M433.75 86.7519L447.689 92.5L433.75 98.2481L433.75 86.7519Z' stroke='black' />
			<path id='Polygon 2_19' d='M461.25 86.7519L447.311 92.5L461.25 98.2481L461.25 86.7519Z' stroke='black' />
			<line id='Line 6_12' x1='441' y1='81.5' x2='454' y2='81.5' stroke='black' />
			<line id='Line 1_19' x1='446.5' y1='93' x2='446.5' y2='81' stroke='black' />
			<line id='Line 2_19' x1='448.5' y1='93' x2='448.5' y2='81' stroke='black' />
		</g>
		<g id='cvalve/closed_9'>
			<path id='Polygon 1_20' d='M433.75 140.752L447.689 146.5L433.75 152.248L433.75 140.752Z' stroke='black' />
			<path id='Polygon 2_20' d='M461.25 140.752L447.311 146.5L461.25 152.248L461.25 140.752Z' stroke='black' />
			<line id='Line 6_13' x1='441' y1='135.5' x2='454' y2='135.5' stroke='black' />
			<line id='Line 1_20' x1='446.5' y1='147' x2='446.5' y2='135' stroke='black' />
			<line id='Line 2_20' x1='448.5' y1='147' x2='448.5' y2='135' stroke='black' />
		</g>
		<g id='cvalve/closed_10'>
			<path id='Polygon 1_21' d='M433.75 32.7519L447.689 38.5L433.75 44.2481L433.75 32.7519Z' stroke='black' />
			<path id='Polygon 2_21' d='M461.25 32.7519L447.311 38.5L461.25 44.2481L461.25 32.7519Z' stroke='black' />
			<line id='Line 6_14' x1='441' y1='27.5' x2='454' y2='27.5' stroke='black' />
			<line id='Line 1_21' x1='446.5' y1='39' x2='446.5' y2='27' stroke='black' />
			<line id='Line 2_21' x1='448.5' y1='39' x2='448.5' y2='27' stroke='black' />
		</g>
		<line id='Line 17' x1='414' y1='311' x2='434' y2='311' stroke='black' stroke-width='2' />
		<line id='Line 21' x1='414' y1='257' x2='434' y2='257' stroke='black' stroke-width='2' />
		<line id='Line 25' x1='414' y1='93' x2='434' y2='93' stroke='black' stroke-width='2' />
		<line id='Line 33' x1='414' y1='147' x2='434' y2='147' stroke='black' stroke-width='2' />
		<line id='Line 29' x1='414' y1='39' x2='434' y2='39' stroke='black' stroke-width='2' />
		<line id='Line 18' x1='461' y1='311' x2='494' y2='311' stroke='black' stroke-width='2' />
		<line id='Line 22' x1='461' y1='257' x2='494' y2='257' stroke='black' stroke-width='2' />
		<line id='Line 26' x1='461' y1='93' x2='494' y2='93' stroke='black' stroke-width='2' />
		<line id='Line 34' x1='461' y1='147' x2='494' y2='147' stroke='black' stroke-width='2' />
		<line id='Line 38' x1='414' y1='203' x2='494' y2='203' stroke='black' stroke-width='2' />
		<line id='Line 30' x1='461' y1='39' x2='494' y2='39' stroke='black' stroke-width='2' />
		<line id='Line 19' x1='526' y1='311' x2='538' y2='311' stroke='black' stroke-width='2' />
		<line id='Line 23' x1='526' y1='257' x2='538' y2='257' stroke='black' stroke-width='2' />
		<line id='Line 27' x1='526' y1='93' x2='538' y2='93' stroke='black' stroke-width='2' />
		<path id='Line 35' d='M529 147H538' stroke='black' stroke-width='2' />
		<line id='Line 31' x1='526' y1='39' x2='538' y2='39' stroke='black' stroke-width='2' />
		<line id='Line 20' x1='565' y1='311' x2='607' y2='311' stroke='black' stroke-width='2' />
		<line id='Line 24' x1='565' y1='257' x2='607' y2='257' stroke='black' stroke-width='2' />
		<line id='Line 28' x1='565' y1='93' x2='607' y2='93' stroke='black' stroke-width='2' />
		<line id='Line 36' x1='565' y1='147' x2='607' y2='147' stroke='black' stroke-width='2' />
		<line id='Line 40' x1='526' y1='203' x2='607' y2='203' stroke='black' stroke-width='2' />
		<line id='Line 32' x1='565' y1='39' x2='607' y2='39' stroke='black' stroke-width='2' />
		<path id='Vector 9' d='M33 38H1V133.227V458' stroke='black' stroke-width='2' />
		<g id='consumer_5'>
			<g id='Property 1=Default_2'>
				<rect id='Rectangle 4_5' x='492.707' y='310.678' width='24' height='24' transform='rotate(-45 492.707 310.678)'
							stroke='black' />
				<line id='Line 16_5' x1='493' y1='310.5' x2='526' y2='310.5' stroke='black' />
				<path id='Vector 5_5'
							d='M510 311L512.887 306L507.113 306L510 311ZM509.5 294L509.5 306.5L510.5 306.5L510.5 294L509.5 294Z'
							fill='black' />
				<path id='Vector 6_5' d='M510 310L507.113 315H512.887L510 310ZM510.5 327V314.5H509.5V327H510.5Z' fill='black' />
				<text id='6_5' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
							letter-spacing='0em'><tspan x='512.132' y='293.091'>6</tspan></text>
			</g>
		</g>
		<g id='consumer/weird'>
			<path id='Vector 7' d='M497.5 135.5H493V161H497' stroke='black' />
			<path id='Vector 8' d='M524 135.5H528.5V161H524.5' stroke='black' />
			<text id='3' fill='black' xml:space='preserve' style='white-space: pre' font-family='Inter' font-size='14'
						letter-spacing='0em'><tspan x='512.043' y='130.091'>3</tspan></text>
		</g>
		<line id='Line 41' x1='1' y1='133' x2='33' y2='133' stroke='black' stroke-width='2' />
		<path id='Vector 11' d='M85 323.5V308.5H121.5' stroke='black' stroke-width='2' />
		<line id='Line 42' x1='1' y1='226' x2='33' y2='226' stroke='black' stroke-width='2' />
		<line id='Line 44' x1='149' y1='308' x2='174' y2='308' stroke='black' stroke-width='2' />
		<path id='Vector 14' d='M228 177.5H252.5V133.5' stroke='black' stroke-width='2' />
		<line id='Line 43' x1='1' y1='413' x2='22' y2='413' stroke='black' stroke-width='2' />
		<path id='Vector 10' d='M49 413H85V396' stroke='black' stroke-width='2' />
		<line id='Line 45' x1='316' y1='38' x2='316' y2='62' stroke='black' stroke-width='2' />
		<line id='Line 46' x1='175' y1='39' x2='175' y2='426' stroke='black' stroke-width='2' />
		<path id='Vector 12' d='M174 426L316.5 424.5V405' stroke='black' stroke-width='2' />
		<path id='Vector 13' d='M316.5 377.5V363' stroke='black' stroke-width='2' />
		<line id='Line 47' x1='174' y1='177' x2='201' y2='177' stroke='black' stroke-width='2' />
		<line id='Line 48' x1='174' y1='177' x2='201' y2='177' stroke='black' stroke-width='2' />
		<path id='Vector 15' d='M316.5 290.5V275' stroke='black' stroke-width='2' />
		<path id='Vector 16' d='M382.5 343.5V232H316V219.5V247.5' stroke='black' stroke-width='2' />
		<path id='Vector 17' d='M316.5 193V176' stroke='black' stroke-width='2' />
		<path id='Vector 18' d='M316.5 103V89' stroke='black' stroke-width='2' />
		<line id='Line 49' x1='415' y1='38' x2='415' y2='343' stroke='black' stroke-width='2' />
		<line id='Line 50' x1='608' y1='38' x2='608' y2='457' stroke='black' stroke-width='2' />
		<line id='Line 51' x1='1' y1='457' x2='609' y2='457' stroke='black' stroke-width='2' />
	</g>
</svg>
