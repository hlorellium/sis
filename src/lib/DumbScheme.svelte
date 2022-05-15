<script lang="ts">
	import type { PumpStates } from './models/PumpStates';

	// State of each pump
	let statePump1: PumpStates = 'off';
	let statePump2: PumpStates = 'off';
	let statePump3: PumpStates = 'off';

	let pressureDropPump1 = 0;
	let pressureDropPump2 = 0;
	let pressureDropPump3 = 0;

	// Is valve openned
	let v1 = true;
	let v2 = true;
	let v3 = false;
	let v4 = false;
	let v5 = false;
	let v6 = false;
	let v7 = false;

	// Is Heat Exchanger working
	$: TO1 = v1 && v2;
	$: TO2 = v3 && v4;

	$: TO = TO1 || TO2;

	// For convenience variables to check if pump is working
	$: pump1Working = statePump1 !== 'off';
	$: pump2Working = statePump2 !== 'off';
	$: pump3Working = statePump3 !== 'off';

	// Is valve openned to nourish the system from reserve tank
	$: nourishing = v7;

	$: waterForPumps = TO || nourishing;

	$: pumpWorking = pump1Working || pump2Working || pump3Working;

	$: isCoolingConsumers = pumpWorking && waterForPumps;

	// Is filter working
	$: filter = v5 && v6;

	const signColor = (isWorking: boolean) => {
		return isWorking ? '#4AFF7D' : 'white';
	};

	const pipeColor = (hasWater: boolean) => {
		return hasWater ? '#00A3FF' : '#7BD0FF';
	};
</script>

<svg id="scheme-container" viewBox="0 0 683 546" fill="none" xmlns="http://www.w3.org/2000/svg">
	<g id="scheme">
		<g id="tank">
			<rect width="80" height="109" transform="translate(279 66)" fill="white" />
			<rect id="Rectangle 5" x="279.5" y="66.5" width="79" height="108" rx="4.5" stroke="black" />
			<rect id="Rectangle 8" x="279.5" y="66.5" width="79" height="108" rx="4.5" stroke="black" />
			<g id="Group 1">
				<rect id="Rectangle 7" x="339" y="129.683" width="8" height="34.5167" fill="#7BFD80" />
				<rect id="Rectangle 6" x="339.5" y="77.5" width="7" height="86.2" stroke="black" />
			</g>
			<text
				id="&#208;&#160;&#208;&#166;&#208;&#159;&#208;&#146;"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="14"
				letter-spacing="0em"><tspan x="279" y="60.5909">&#x420;&#x411; III&#x43a;</tspan></text
			>
			<path
				id="Polygon 3"
				d="M311.139 90.75L318.5 78L325.861 90.75H311.139Z"
				fill="#FBFF40"
				stroke="black"
			/>
			<path
				id="Polygon 4"
				d="M311.139 150.25L318.5 163L325.861 150.25H311.139Z"
				fill="#FBFF40"
				stroke="black"
			/>
			<g id="Group 2">
				<text
					id="35.82"
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="10"
					letter-spacing="0em"><tspan x="297.538" y="124.136">35.82</tspan></text
				>
				<rect id="Rectangle 10" x="294.5" y="113.5" width="33" height="14" stroke="black" />
				<text
					id="%"
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="10"
					font-weight="bold"
					letter-spacing="0em"><tspan x="328.703" y="124.136">%</tspan></text
				>
			</g>
		</g>
		<rect
			id="pump2 cooling"
			y="163"
			width="95"
			height="12"
			fill={pipeColor(pump2Working && waterForPumps)}
		/>
		<rect
			id="pump r cooling"
			y="265"
			width="95"
			height="12"
			fill={pipeColor(pump3Working && waterForPumps)}
		/>
		<rect
			id="pump 2 or 1 cooling"
			x="12"
			y="175"
			width="102"
			height="12"
			transform="rotate(90 12 175)"
			fill={pipeColor((pump1Working || pump2Working) && waterForPumps)}
		/>
		<rect id="v7 pumps" x="230" y="206" width="37" height="12" fill={pipeColor(nourishing)} />
		<g id="f v6">
			<path d="M128 322L128 343H116L116 322L128 322Z" fill={pipeColor(isCoolingConsumers && v5)} />
			<path d="M116 318H160V330H116V318Z" fill={pipeColor(isCoolingConsumers && v5)} />
		</g>
		<rect
			id="v6 pumps"
			x="207"
			y="318"
			width="34"
			height="12"
			fill={pipeColor(isCoolingConsumers && v5 && v6)}
		/>
		<rect id="pump v5" y="418" width="37" height="12" fill={pipeColor(isCoolingConsumers)} />
		<g id="v5 f">
			<path d="M116 426V405L128 405V426H116Z" fill={pipeColor(isCoolingConsumers && v5)} />
			<path d="M128 430H84V418H128V430Z" fill={pipeColor(isCoolingConsumers && v5)} />
		</g>
		<g id="rb v7">
			<path d="M316 206H337V218H316V206Z" fill={pipeColor(true)} />
			<path d="M337 218L337 175L349 175V218H337Z" fill={pipeColor(true)} />
		</g>
		<g id="pumps">
			<path d="M186 23H242V35H186V23Z" fill={pipeColor(TO || nourishing)} />
			<path d="M183 123H241V135H183V123Z" fill={pipeColor(TO || nourishing)} />
			<path d="M184 226H242V238H184V226Z" fill={pipeColor(TO || nourishing)} />
			<path d="M242 23V238H230L230 23H242Z" fill={pipeColor(TO || nourishing)} />
		</g>
		<g id="v4 pumps">
			<path d="M415 494V514H403V494H415Z" fill={pipeColor(TO2)} />
			<path d="M230 502H415V514H230V502Z" fill={pipeColor(TO2)} />
			<path d="M242 238L242 514H230L230 238L242 238Z" fill={pipeColor(TO2)} />
		</g>
		<g id="SVZ pipes">
			<path d="M402 263H480V275H402V263Z" fill={pipeColor(true)} />
			<path d="M483 263L483 425H471L471 263H483Z" fill={pipeColor(true)} />
			<path d="M414 243L414 263H402L402 243L414 243Z" fill={pipeColor(true)} />
			<path d="M414 275L414 295H402L402 275H414Z" fill={pipeColor(true)} />
		</g>
		<rect
			id="TO1 V2"
			x="414"
			y="92"
			width="20"
			height="12"
			transform="rotate(90 414 92)"
			fill={pipeColor(v1)}
		/>
		<g id="v2 pumps">
			<path d="M242 23H414V35H242V23Z" fill={pipeColor(TO1)} />
			<path d="M414 25V42H402V25L414 25Z" fill={pipeColor(TO1)} />
		</g>
		<rect
			id="TO2 v4"
			x="415"
			y="425"
			width="20"
			height="12"
			transform="rotate(90 415 425)"
			fill={pipeColor(v3)}
		/>
		<rect
			id="v1 TO1"
			x="414"
			y="174"
			width="20"
			height="12"
			transform="rotate(90 414 174)"
			fill={pipeColor(v1)}
		/>
		<rect
			id="v3 TO2"
			x="414"
			y="345"
			width="20"
			height="12"
			transform="rotate(90 414 345)"
			fill={pipeColor(v3)}
		/>
		<g id="pumps cooling">
			<path d="M521 24V425H509L509 24L521 24Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M511 23H566V35H511V23Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M509 95H564V107H509V95Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M512 167H567V179H512V167Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M511 238H566V250H511V238Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M512 309H567V321H512V309Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M511 380H566V392H511V380Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M625 95H680V107H625V95Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M628 167H683V179H628V167Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M627 238H682V250H627V238Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M628 309H683V321H628V309Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M627 380H682V392H627V380Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M683 23V546H671V23L683 23Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M681 546L0 546L1.04907e-06 534L681 534V546Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M628 23H683V35H628V23Z" fill={pipeColor(isCoolingConsumers)} />
			<path d="M12 277L12 546L0 546L3.02359e-06 277H12Z" fill={pipeColor(isCoolingConsumers)} />
		</g>
		<g id="pump1 cooling">
			<path d="M0 60H12V175H0V60Z" fill={pipeColor(pump1Working && waterForPumps)} />
			<path d="M0 60H95V72H0V60Z" fill={pipeColor(pump1Working && waterForPumps)} />
		</g>
		<g id="valve" on:click={() => (v7 = !v7)}>
			<path
				id="Vector 21"
				d="M267 226V197L290.5 204.5V219L267 226Z"
				fill={signColor(v7)}
				stroke="black"
			/>
			<path
				id="Vector 22"
				d="M316.5 226V197L293 204.5V219L316.5 226Z"
				fill={signColor(v7)}
				stroke="black"
			/>
			<text
				id="V1"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"><tspan x="267" y="193.364">&#x41a;7</tspan></text
			>
		</g>
		<g id="valve_2" on:click={() => (v2 = !v2)}>
			<path
				id="Vector 21_2"
				d="M394 42L423 42L415.5 65.5L401 65.5L394 42Z"
				fill={signColor(v2)}
				stroke="black"
			/>
			<path
				id="Vector 22_2"
				d="M394 91.5L423 91.5L415.5 68L401 68L394 91.5Z"
				fill={signColor(v2)}
				stroke="black"
			/>
			<text
				id="V1_2"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"><tspan x="427" y="53.3636">&#x41a;2</tspan></text
			>
		</g>
		<g id="valve_3" on:click={() => (v4 = !v4)}>
			<path
				id="Vector 21_3"
				d="M394 444L423 444L415.5 467.5L401 467.5L394 444Z"
				fill={signColor(v4)}
				stroke="black"
			/>
			<path
				id="Vector 22_3"
				d="M394 493.5L423 493.5L415.5 470L401 470L394 493.5Z"
				fill={signColor(v4)}
				stroke="black"
			/>
			<text
				id="V1_3"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"><tspan x="427" y="455.364">&#x41a;4</tspan></text
			>
		</g>
		<g id="valve_4" on:click={() => (v1 = !v1)}>
			<path
				id="Vector 21_4"
				d="M395 194L424 194L416.5 217.5L402 217.5L395 194Z"
				fill={signColor(v1)}
				stroke="black"
			/>
			<path
				id="Vector 22_4"
				d="M395 243.5L424 243.5L416.5 220L402 220L395 243.5Z"
				fill={signColor(v1)}
				stroke="black"
			/>
			<text
				id="V1_4"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"><tspan x="428" y="205.364">&#x41a;1</tspan></text
			>
		</g>
		<g id="valve_5" on:click={() => (v3 = !v3)}>
			<path
				id="Vector 21_5"
				d="M394 295L423 295L415.5 318.5L401 318.5L394 295Z"
				fill={signColor(v3)}
				stroke="black"
			/>
			<path
				id="Vector 22_5"
				d="M394 344.5L423 344.5L415.5 321L401 321L394 344.5Z"
				fill={signColor(v3)}
				stroke="black"
			/>
			<text
				id="V1_5"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"><tspan x="427" y="306.364">&#x41a;3</tspan></text
			>
		</g>
		<g id="to">
			<path
				id="Polygon 5"
				d="M373.993 123.555L409 105.562L444.007 123.555V159.445L409 177.438L373.993 159.445V123.555Z"
				fill={signColor(TO1)}
				stroke="black"
			/>
			<text
				id="&#208;&#162;&#208;&#158; III-IV &#208;&#186; &#226;&#132;&#150;1"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="10"
				letter-spacing="0em"
				><tspan x="375.995" y="145.636">&#x422;&#x41e; III-IV &#x43a; &#x2116;1</tspan></text
			>
		</g>
		<g id="to_2">
			<path
				id="Polygon 5_2"
				d="M372.993 379.555L408 361.562L443.007 379.555V415.445L408 433.438L372.993 415.445V379.555Z"
				fill={signColor(TO2)}
				stroke="black"
			/>
			<text
				id="&#208;&#162;&#208;&#158; III-IV &#208;&#186; &#226;&#132;&#150;1_2"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="10"
				letter-spacing="0em"
				><tspan x="374.292" y="401.636">&#x422;&#x41e; III-IV &#x43a; &#x2116;2</tspan></text
			>
		</g>
		<g id="reserve tank">
			<rect
				id="Rectangle 38"
				x="450.5"
				y="425.5"
				width="89"
				height="59"
				fill="white"
				stroke="black"
			/>
			<text
				id="&#208;&#145;&#208;&#176;&#208;&#186; &#208;&#161;&#208;&#146;&#208;&#151;"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"
				><tspan x="470.666" y="459.364">&#x411;&#x430;&#x43a; &#x421;&#x412;&#x417;</tspan></text
			>
		</g>
		<g id="consumer">
			<rect
				id="Rectangle 38_2"
				x="566.5"
				y="8.5"
				width="61"
				height="40.3333"
				fill="white"
				stroke="black"
			/>
			<text
				id="&#208;&#159;&#208;&#190;&#209;&#130;&#209;&#128;. 1"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"
				><tspan x="576.34" y="33.0303">&#x41f;&#x43e;&#x442;&#x440;. 1</tspan></text
			>
		</g>
		<g id="consumer_2">
			<rect
				id="Rectangle 38_3"
				x="564.5"
				y="80.5"
				width="61"
				height="40.3333"
				fill="white"
				stroke="black"
			/>
			<text
				id="&#208;&#159;&#208;&#190;&#209;&#130;&#209;&#128;. 1_2"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"
				><tspan x="573.496" y="105.03">&#x41f;&#x43e;&#x442;&#x440;. 2</tspan></text
			>
		</g>
		<g id="consumer_3">
			<rect
				id="Rectangle 38_4"
				x="566.5"
				y="152.5"
				width="61"
				height="40.3333"
				fill="white"
				stroke="black"
			/>
			<text
				id="&#208;&#159;&#208;&#190;&#209;&#130;&#209;&#128;. 1_3"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"
				><tspan x="575.309" y="177.03">&#x41f;&#x43e;&#x442;&#x440;. 3</tspan></text
			>
		</g>
		<g id="consumer_4">
			<rect
				id="Rectangle 38_5"
				x="566.5"
				y="224.5"
				width="61"
				height="40.3333"
				fill="white"
				stroke="black"
			/>
			<text
				id="&#208;&#159;&#208;&#190;&#209;&#130;&#209;&#128;. 1_4"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"
				><tspan x="575.279" y="249.03">&#x41f;&#x43e;&#x442;&#x440;. 4</tspan></text
			>
		</g>
		<g id="consumer_5">
			<rect
				id="Rectangle 38_6"
				x="566.5"
				y="296.5"
				width="61"
				height="40.3333"
				fill="white"
				stroke="black"
			/>
			<text
				id="&#208;&#159;&#208;&#190;&#209;&#130;&#209;&#128;. 1_5"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"
				><tspan x="575.479" y="321.03">&#x41f;&#x43e;&#x442;&#x440;. 5</tspan></text
			>
		</g>
		<g id="consumer_6">
			<rect
				id="Rectangle 38_7"
				x="566.5"
				y="368.5"
				width="61"
				height="40.3333"
				fill="white"
				stroke="black"
			/>
			<text
				id="&#208;&#159;&#208;&#190;&#209;&#130;&#209;&#128;. 1_6"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"
				><tspan x="575.385" y="393.03">&#x41f;&#x43e;&#x442;&#x440;. 6</tspan></text
			>
		</g>
		<g id="Pump" on:click={() => (pump1Working ? (statePump1 = 'off') : (statePump1 = 'HS'))}>
			<path
				id="Ellipse 3"
				d="M139 72.5C122.708 72.5 109.5 59.2924 109.5 43C109.5 26.7076 122.708 13.5 139 13.5C155.292 13.5 168.5 26.7076 168.5 43C168.5 59.2924 155.292 72.5 139 72.5Z"
				fill={signColor(pump1Working)}
				stroke="black"
			/>
			<path
				id="Vector 19"
				d="M186 42L167.5 35.5C163.9 20.7 150.667 15 144.5 14L186 14L186 42Z"
				fill={signColor(pump1Working)}
				stroke="black"
			/>
			<path
				id="Vector 20"
				d="M94.9999 72.5L138 72.5C122 72 112.833 59.5 111.5 54L95 60L94.9999 72.5Z"
				fill={signColor(pump1Working)}
				stroke="black"
			/>
			<text
				id="&#208;&#166;&#208;&#157; III-1"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"><tspan x="95" y="8.86364">&#x426;&#x41d; III-1</tspan></text
			>
		</g>
		<g id="Pump_2" on:click={() => (pump2Working ? (statePump2 = 'off') : (statePump2 = 'HS'))}>
			<path
				id="Ellipse 3_2"
				d="M136 174.5C119.708 174.5 106.5 161.292 106.5 145C106.5 128.708 119.708 115.5 136 115.5C152.292 115.5 165.5 128.708 165.5 145C165.5 161.292 152.292 174.5 136 174.5Z"
				fill={signColor(pump2Working)}
				stroke="black"
			/>
			<path
				id="Vector 19_2"
				d="M183 144L164.5 137.5C160.9 122.7 147.667 117 141.5 116L183 116L183 144Z"
				fill={signColor(pump2Working)}
				stroke="black"
			/>
			<path
				id="Vector 20_2"
				d="M91.9999 174.5L135 174.5C119 174 109.833 161.5 108.5 156L92 162L91.9999 174.5Z"
				fill={signColor(pump2Working)}
				stroke="black"
			/>
			<text
				id="&#208;&#166;&#208;&#157; III-1_2"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"><tspan x="92" y="110.864">&#x426;&#x41d; III-2</tspan></text
			>
		</g>
		<g id="Pump_3" on:click={() => (pump3Working ? (statePump3 = 'off') : (statePump3 = 'HS'))}>
			<path
				id="Ellipse 3_3"
				d="M139 276.5C122.708 276.5 109.5 263.292 109.5 247C109.5 230.708 122.708 217.5 139 217.5C155.292 217.5 168.5 230.708 168.5 247C168.5 263.292 155.292 276.5 139 276.5Z"
				fill={signColor(pump3Working)}
				stroke="black"
			/>
			<path
				id="Vector 19_3"
				d="M186 246L167.5 239.5C163.9 224.7 150.667 219 144.5 218L186 218L186 246Z"
				fill={signColor(pump3Working)}
				stroke="black"
			/>
			<path
				id="Vector 20_3"
				d="M94.9999 276.5L138 276.5C122 276 112.833 263.5 111.5 258L95 264L94.9999 276.5Z"
				fill={signColor(pump3Working)}
				stroke="black"
			/>
			<text
				id="&#208;&#166;&#208;&#157; III-1_3"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"><tspan x="95" y="212.864">&#x426;&#x41d; III-&#x420;</tspan></text
			>
		</g>
		<g id="valve_6" on:click={() => (v6 = !v6)}>
			<path
				id="Vector 21_6"
				d="M158 338V309L181.5 316.5V331L158 338Z"
				fill={signColor(v6)}
				stroke="black"
			/>
			<path
				id="Vector 22_6"
				d="M207.5 338V309L184 316.5V331L207.5 338Z"
				fill={signColor(v6)}
				stroke="black"
			/>
			<text
				id="V1_6"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"><tspan x="158" y="305.364">&#x41a;6</tspan></text
			>
		</g>
		<g id="valve_7" on:click={() => (v5 = !v5)}>
			<path
				id="Vector 21_7"
				d="M35 438V409L58.5 416.5V431L35 438Z"
				fill={signColor(v5)}
				stroke="black"
			/>
			<path
				id="Vector 22_7"
				d="M84.5 438V409L61 416.5V431L84.5 438Z"
				fill={signColor(v5)}
				stroke="black"
			/>
			<text
				id="V1_7"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"><tspan x="35" y="405.364">&#x41a;5</tspan></text
			>
		</g>
		<g id="filter">
			<path
				id="Vector 21_8"
				d="M139 376.431L104 376.431L116.672 405L126.931 405L139 376.431Z"
				fill={signColor(filter)}
				stroke="black"
			/>
			<path
				id="Vector 22_8"
				d="M139 371.569L104 371.569L116.672 343L126.931 343L139 371.569Z"
				fill={signColor(filter)}
				stroke="black"
			/>
			<path id="Line 52" d="M103 374L139.5 374" stroke="black" stroke-dasharray="3 3" />
			<text
				id="Filter"
				fill="black"
				xml:space="preserve"
				style="white-space: pre"
				font-family="Inter"
				font-size="12"
				letter-spacing="0em"
				><tspan x="139" y="356.364">&#x424;&#x418;&#x41e; III&#x43a;</tspan></text
			>
		</g>
	</g>
</svg>

<style>
	#scheme-container {
		width: 100%;
	}
</style>
