<script lang="ts">
	import { onMount } from 'svelte';
	import { COOLING_STEP } from './consts/simulation';
	import Textfield from '@smui/textfield';
	import Tab, { Label } from '@smui/tab';
	import Button from '@smui/button';

	import TabBar from '@smui/tab-bar';
	import HelperText from '@smui/textfield/helper-text';
	import Radio from '@smui/radio';
	import FormField from '@smui/form-field';

	import type { PumpStates } from './models/PumpStates';

	let active = 'Параметры насосов';

	const pumpStates = ['HS', 'LS', 'off'];

	// Pumps errors
	let CN1E = false;
	let CN2E = false;
	let CN3E = false;

	// Heat Exchanger errors
	let TO1E = false;
	let TO2E = false;
	$: TOE = TO1E || TO2E;

	// State of each pump
	let statePump1: PumpStates = 'LS';
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

	let pumpState: PumpStates;

	$: pumpState = pump1Working
		? statePump1
		: pump2Working
		? statePump2
		: pump3Working
		? statePump3
		: 'off';

	// Is valve openned to nourish the system from reserve tank
	$: nourishing = v7;

	$: waterForPumps = TO;

	$: pumpWorking = pump1Working || pump2Working || pump3Working;

	$: isCoolingConsumers = pumpWorking && waterForPumps;

	// Is filter working
	$: filter = v5 && v6;

	// Uitility functions
	const signColor = (isWorking: boolean) => (isWorking ? '#4AFF7D' : 'white');

	const pipeColor = (hasWater: boolean) => (hasWater ? '#00A3FF' : '#7BD0FF');

	const activeDirectionColor = (isActive: boolean) => (isActive ? '#F2990C' : '#FBFF20');

	const heightOffset = (percentage: number, height: number) => height * (percentage / 100);

	const coolingSpeed = (mode: PumpStates) => {
		switch (mode) {
			case 'HS':
				return 'Большая скорость';
			case 'LS':
				return 'Малая скорость';
			default:
				return 'Охлаждение отсутствует';
		}
	};

	let rbLevel = 50;

	const rbChangeSpeed = 1;

	const rbMaxLevel = 100;
	const rbMinLevel = 0;

	$: rbLevelDecresing = nourishing && rbLevel > rbMinLevel;
	$: rbLevelIncreasing = !nourishing && rbLevel < rbMaxLevel;

	// Consumers temperature
	let C1T = 25;
	let C2T = 25;
	let C3T = 25;
	let C4T = 25;
	let C5T = 25;
	let C6T = 25;

	let C1Coef = 1.1;
	let C2Coef = 1.1;
	let C3Coef = 1.1;
	let C4Coef = 1.1;
	let C5Coef = 1.1;
	let C6Coef = 1.1;

	// React to accidents
	$: if (CN1E && statePump1 !== 'off') {
		if (!CN2E) {
			statePump2 = statePump1;
		} else if (!CN3E) {
			statePump3 = statePump1;
		}

		statePump1 = 'off';
	}

	$: if (CN2E && statePump2 !== 'off') {
		if (!CN1E) {
			statePump1 = statePump2;
		} else if (!CN3E) {
			statePump3 = statePump2;
		}

		statePump2 = 'off';
	}

	$: if (CN3E && statePump3 !== 'off') {
		if (!CN1E) {
			statePump1 = statePump3;
		} else if (!CN2E) {
			statePump2 = statePump3;
		}

		statePump3 = 'off';
	}

	$: if (TO1E) {
		TO1 = false;
		v1 = false;
		v2 = false;

		if (!TO2E) {
			v3 = true;
			v4 = true;
		}
	}

	$: if (TO2E) {
		TO2 = false;
		if (!TO1E) {
			v1 = true;
			v2 = true;
		}
		v3 = false;
		v4 = false;
	}

	let val = 'HS';

	// Simulate circuit working
	const updateRbLevel = () => {
		if (rbLevelDecresing) {
			rbLevel = rbLevel - rbChangeSpeed;
		} else if (rbLevelIncreasing) {
			rbLevel = rbLevel + rbChangeSpeed;
		}
	};

	const updateTemperature = (
		currentTemperature: number,
		consumerCoef: number,
		coolingStatus: PumpStates
	): number => {
		const noiseCoef = Math.random() * (1.4 + 0.15) - 0.15;

		const coolingCoef = coolingStatus === 'HS' ? 2 : coolingStatus === 'LS' ? 1 : -1;

		const newTemp =
			Math.round(
				(currentTemperature - COOLING_STEP * (coolingCoef / 10) * noiseCoef * consumerCoef) * 100
			) / 100;

		return newTemp > 0 ? newTemp : 0;
	};

	function updateConsumersTemperatures() {
		C1T = updateTemperature(C1T, C1Coef || 1, pumpState);
		C2T = updateTemperature(C2T, 1.15, pumpState);
		C3T = updateTemperature(C3T, 1.12, pumpState);
		C4T = updateTemperature(C4T, 1.11, pumpState);
		C5T = updateTemperature(C5T, 1.1, pumpState);
		C6T = updateTemperature(C6T, 1.05, pumpState);
	}

	function update() {
		updateRbLevel();
		updateConsumersTemperatures();
	}

	onMount(() => {
		setInterval(update, 100);
	});
</script>

<div class="container">
	<div class="left-side">
		<div class="cooling-mode">
			<span>Скорость охлаждения: </span><span>{coolingSpeed(pumpState)}</span>
		</div>

		<TabBar tabs={['Параметры насосов', 'Параметры потребителей']} let:tab bind:active>
			<Tab {tab} minWidth>
				<Label>{tab}</Label>
			</Tab>
		</TabBar>

		{#if active === 'Параметры насосов'}
			<div class="pumps-params">
				<div>
					<span> Режим работы ЦН III-1 </span>
					{#each pumpStates as option}
						<FormField>
							<Radio bind:group={statePump1} value={option} />
							<span slot="label">{option}</span>
						</FormField>
					{/each}
				</div>
				<div>
					<span> Режим работы ЦН III-2 </span>
					{#each pumpStates as option}
						<FormField>
							<Radio bind:group={statePump2} value={option} />
							<span slot="label">{option}</span>
						</FormField>
					{/each}
				</div>
				<div>
					<span> Режим работы ЦН III-Р </span>
					{#each pumpStates as option}
						<FormField>
							<Radio bind:group={statePump3} value={option} />
							<span slot="label">{option}</span>
						</FormField>
					{/each}
				</div>
			</div>
		{/if}

		{#if active === 'Параметры потребителей'}
			<Textfield bind:value={C1Coef} label="Коэффицент Потр. 1" type="number" input$step="0.1">
				<HelperText slot="helper">Коэффицент охлаждения Потр. 1</HelperText>
			</Textfield>

			<Textfield bind:value={C2Coef} label="Коэффицент Потр. 2" type="number" input$step="0.1">
				<HelperText slot="helper">Коэффицент охлаждения Потр. 2</HelperText>
			</Textfield>

			<Textfield bind:value={C3Coef} label="Коэффицент Потр. 3" type="number" input$step="0.1">
				<HelperText slot="helper">Коэффицент охлаждения Потр. 3</HelperText>
			</Textfield>

			<Textfield bind:value={C4Coef} label="Коэффицент Потр. 4" type="number" input$step="0.1">
				<HelperText slot="helper">Коэффицент охлаждения Потр. 4</HelperText>
			</Textfield>

			<Textfield bind:value={C5Coef} label="Коэффицент Потр. 5" type="number" input$step="0.1">
				<HelperText slot="helper">Коэффицент охлаждения Потр. 5</HelperText>
			</Textfield>

			<Textfield bind:value={C6Coef} label="Коэффицент Потр. 6" type="number" input$step="0.1">
				<HelperText slot="helper">Коэффицент охлаждения Потр. 6</HelperText>
			</Textfield>
		{/if}
	</div>

	<svg
		width="683"
		height="577"
		viewBox="0 0 683 577"
		fill="none"
		xmlns="http://www.w3.org/2000/svg"
	>
		<g id="scheme">
			<g id="tank">
				<rect width="80" height="109" transform="translate(279 97.0002)" fill="white" />
				<rect
					id="Rectangle 5"
					x="279.5"
					y="97.5002"
					width="79"
					height="108"
					rx="4.5"
					stroke="black"
				/>
				<rect
					id="Rectangle 8"
					x="279.5"
					y="97.5002"
					width="79"
					height="108"
					rx="4.5"
					stroke="black"
				/>
				<g id="Group 1">
					<rect
						id="Rectangle 7"
						x="339"
						y={194.7 - heightOffset(rbLevel, 86.2)}
						width="8"
						height={heightOffset(rbLevel, 86.2)}
						fill="#7BFD80"
					/>
					<rect id="Rectangle 6" x="339.5" y="108.5" width="7" height="86.2" stroke="black" />
				</g>
				<text
					id="&#208;&#160;&#208;&#166;&#208;&#159;&#208;&#146;"
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="14"
					letter-spacing="0em"><tspan x="279" y="91.5912">&#x420;&#x411; III&#x43a;</tspan></text
				>
				<path
					id="up"
					d="M311.139 121.75L318.5 109L325.861 121.75H311.139Z"
					fill={activeDirectionColor(rbLevelIncreasing)}
					stroke="black"
				/>
				<path
					id="down"
					d="M311.139 181.25L318.5 194L325.861 181.25H311.139Z"
					fill={activeDirectionColor(rbLevelDecresing)}
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
						letter-spacing="0em"><tspan x="297.538" y="155.137">{rbLevel}</tspan></text
					>
					<rect id="Rectangle 10" x="294.5" y="144.5" width="33" height="14" stroke="black" />
					<text
						id="%"
						fill="black"
						xml:space="preserve"
						style="white-space: pre"
						font-family="Inter"
						font-size="10"
						font-weight="bold"
						letter-spacing="0em"><tspan x="328.703" y="155.137">%</tspan></text
					>
				</g>
			</g>

			<g id="pump 1 cooling">
				<rect
					id="pump 2 or 1 cooling_2"
					x="12.0002"
					y="18.0002"
					width="96"
					height="12"
					transform="rotate(90 12.0002 18.0002)"
					fill={pipeColor(pump1Working && waterForPumps)}
				/>
				<rect
					id="pump 2 or 1 cooling_3"
					x="95"
					y="25"
					width="95"
					height="12"
					transform="rotate(-180 95 25)"
					fill={pipeColor(pump1Working && waterForPumps)}
				/>
			</g>
			<rect
				id="pump2 cooling"
				x="0.000244141"
				y="114"
				width="92"
				height="12"
				fill={pipeColor(pump2Working && waterForPumps)}
			/>
			<rect
				id="pump r cooling"
				x="0.000244141"
				y="215"
				width="95"
				height="12"
				fill={pipeColor(pump3Working && waterForPumps)}
			/>
			<rect
				id="pump 2 or 1 cooling"
				x="12.0002"
				y="114"
				width="194"
				height="12"
				transform="rotate(90 12.0002 114)"
				fill={pipeColor((pump1Working || pump2Working) && waterForPumps)}
			/>
			<rect id="v7 pumps" x="230" y="237" width="37" height="12" fill={pipeColor(nourishing)} />
			<g id="f v6">
				<path
					d="M128 353L128 374H116L116 353L128 353Z"
					fill={pipeColor(isCoolingConsumers && v5)}
				/>
				<path d="M116 349H160V361H116V349Z" fill={pipeColor(isCoolingConsumers && v5)} />
			</g>
			<rect
				id="k6 pumps"
				x="207"
				y="349"
				width="34"
				height="12"
				fill={pipeColor(isCoolingConsumers && v5 && v6)}
			/>
			<rect
				id="pump v5"
				x="0.000244141"
				y="449"
				width="37"
				height="12"
				fill={pipeColor(isCoolingConsumers)}
			/>
			<g id="v5 f">
				<path d="M116 457V436L128 436V457H116Z" fill={pipeColor(isCoolingConsumers)} />
				<path d="M128 461H84.0002V449H128V461Z" fill={pipeColor(isCoolingConsumers)} />
			</g>
			<g id="rb v7">
				<path d="M316 237H337V249H316V237Z" fill={pipeColor(true)} />
				<path d="M337 249L337 206L349 206V249H337Z" fill={pipeColor(true)} />
			</g>
			<g id="pumps">
				<path d="M186 54.0002H242V66.0002H186V54.0002Z" fill={pipeColor(TO || nourishing)} />
				<path d="M183 154H241V166H183V154Z" fill={pipeColor(TO || nourishing)} />
				<path d="M184 257H242V269H184V257Z" fill={pipeColor(TO || nourishing)} />
				<path d="M242 54.0002V269H230L230 54.0002H242Z" fill={pipeColor(TO || nourishing)} />
			</g>
			<g id="v4 pumps">
				<path d="M415 525V545H403V525H415Z" fill={pipeColor(TO2)} />
				<path d="M230 533H415V545H230V533Z" fill={pipeColor(TO2)} />
				<path d="M242 269L242 545H230L230 269L242 269Z" fill={pipeColor(TO2)} />
			</g>
			<g id="SVZ pipes">
				<path d="M402 294H480V306H402V294Z" fill={pipeColor(true)} />
				<path d="M483 294L483 456H471L471 294H483Z" fill={pipeColor(true)} />
				<path d="M414 274L414 294H402L402 274L414 274Z" fill={pipeColor(true)} />
				<path d="M414 306L414 326H402L402 306H414Z" fill={pipeColor(true)} />
			</g>
			<rect
				id="TO1 V2"
				x="414"
				y="123"
				width="20"
				height="12"
				transform="rotate(90 414 123)"
				fill={pipeColor(v1)}
			/>
			<g id="v2 pumps">
				<path d="M230 54.0002H414V66.0002H230V54.0002Z" fill={pipeColor(TO1)} />
				<path d="M414 56.0002V73.0002H401.163V56.0002L414 56.0002Z" fill={pipeColor(TO1)} />
			</g>
			<rect
				id="TO2 v4"
				x="415"
				y="456"
				width="20"
				height="12"
				transform="rotate(90 415 456)"
				fill={pipeColor(v3)}
			/>
			<rect
				id="v1 TO1"
				x="414"
				y="205"
				width="20"
				height="12"
				transform="rotate(90 414 205)"
				fill={pipeColor(v1)}
			/>
			<rect
				id="v3 TO2"
				x="414"
				y="376"
				width="20"
				height="12"
				transform="rotate(90 414 376)"
				fill={pipeColor(v3)}
			/>
			<g id="pumps cooling" style="--fillColor: {pipeColor(isCoolingConsumers)}">
				<path d="M521 55.0002V456H509L509 55.0002L521 55.0002Z" fill="var(--fillColor)" />
				<path d="M511 54.0002H566V66.0002H511V54.0002Z" fill="var(--fillColor)" />
				<path d="M509 126H564V138H509V126Z" fill="var(--fillColor)" />
				<path d="M512 198H567V210H512V198Z" fill="var(--fillColor)" />
				<path d="M511 269H566V281H511V269Z" fill="var(--fillColor)" />
				<path d="M512 340H567V352H512V340Z" fill="var(--fillColor)" />
				<path d="M511 411H566V423H511V411Z" fill="var(--fillColor)" />
				<path d="M625 126H680V138H625V126Z" fill="var(--fillColor)" />
				<path d="M628 198H683V210H628V198Z" fill="var(--fillColor)" />
				<path d="M627 269H682V281H627V269Z" fill="var(--fillColor)" />
				<path d="M628 340H683V352H628V340Z" fill="var(--fillColor)" />
				<path d="M627 411H682V423H627V411Z" fill="var(--fillColor)" />
				<path d="M683 54.0002V577H671V54.0002L683 54.0002Z" fill="var(--fillColor)" />
				<path d="M681 577L0.000244141 577L0.00024519 565L681 565V577Z" fill="var(--fillColor)" />
				<path d="M628 54.0002H683V66.0002H628V54.0002Z" fill="var(--fillColor)" />
				<path
					d="M12.0002 215L12.0002 577.5L0.000244141 577.5L0.000247164 215H12.0002Z"
					fill="var(--fillColor)"
				/>
			</g>
			<g id="valve" on:click={() => (v7 = !v7)}>
				<path
					id="Vector 21"
					d="M267 257V228L290.5 235.5V250L267 257Z"
					fill={signColor(v7)}
					stroke="black"
				/>
				<path
					id="Vector 22"
					d="M316.5 257V228L293 235.5V250L316.5 257Z"
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
					letter-spacing="0em"><tspan x="267" y="224.364">&#x41a;7</tspan></text
				>
			</g>
			<g id="valve_2" on:click={() => {
					if (TOE) return;
					v2 = !v2;
				}}>
				<path
					id="Vector 21_2"
					d="M394 73.0001L423 73.0001L415.5 96.5001L401 96.5001L394 73.0001Z"
					fill={signColor(v2)}
					stroke="black"
				/>
				<path
					id="Vector 22_2"
					d="M394 122.5L423 122.5L415.5 99.0001L401 99.0001L394 122.5Z"
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
					letter-spacing="0em"><tspan x="427" y="84.3638">&#x41a;2</tspan></text
				>
			</g>
			<g id="valve_3" on:click={() => {
					if (TOE) return;
					v4 = !v4;
				}}>
				<path
					id="Vector 21_3"
					d="M394 475L423 475L415.5 498.5L401 498.5L394 475Z"
					fill={signColor(v4)}
					stroke="black"
				/>
				<path
					id="Vector 22_3"
					d="M394 524.5L423 524.5L415.5 501L401 501L394 524.5Z"
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
					letter-spacing="0em"><tspan x="427" y="486.364">&#x41a;4</tspan></text
				>
			</g>
			<g id="valve_4" on:click={() => {
					if (TOE) return;
					v1 = !v1;
				}}>
				<path
					id="Vector 21_4"
					d="M395 225L424 225L416.5 248.5L402 248.5L395 225Z"
					fill={signColor(v1)}
					stroke="black"
				/>
				<path
					id="Vector 22_4"
					d="M395 274.5L424 274.5L416.5 251L402 251L395 274.5Z"
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
					letter-spacing="0em"><tspan x="428" y="236.364">&#x41a;1</tspan></text
				>
			</g>
			<g id="valve_5" on:click={() => {
					if (TOE) return;
					v3 = !v3;
				}}>
				<path
					id="Vector 21_5"
					d="M394 326L423 326L415.5 349.5L401 349.5L394 326Z"
					fill={signColor(v3)}
					stroke="black"
				/>
				<path
					id="Vector 22_5"
					d="M394 375.5L423 375.5L415.5 352L401 352L394 375.5Z"
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
					letter-spacing="0em"><tspan x="427" y="337.364">&#x41a;3</tspan></text
				>
			</g>
			<g id="to" class:hasError={TO1E} on:contextmenu|preventDefault={() => (TO1E = !TO1E)}>
				<path
					id="Polygon 5"
					d="M373.993 154.555L409 136.562L444.007 154.555V190.445L409 208.438L373.993 190.445V154.555Z"
					fill={signColor(TO1)}
					stroke="var(--strokeColor)"
					stroke-width="var(--strokeWidth)"
				/>
				<text
					id="&#208;&#162;&#208;&#158; III-IV &#208;&#186; &#226;&#132;&#150;1"
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="10"
					letter-spacing="0em"
					><tspan x="375.995" y="176.637">&#x422;&#x41e; III-IV &#x43a; &#x2116;1</tspan></text
				>
			</g>
			<g id="to_2" class:hasError={TO2E} on:contextmenu|preventDefault={() => (TO2E = !TO2E)}>
				<path
					id="Polygon 5_2"
					d="M372.993 410.555L408 392.562L443.007 410.555V446.445L408 464.438L372.993 446.445V410.555Z"
					fill={signColor(TO2)}
					stroke="var(--strokeColor)"
					stroke-width="var(--strokeWidth)"
				/>
				<text
					id="&#208;&#162;&#208;&#158; III-IV &#208;&#186; &#226;&#132;&#150;1_2"
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="10"
					letter-spacing="0em"
					><tspan x="374.292" y="432.636">&#x422;&#x41e; III-IV &#x43a; &#x2116;2</tspan></text
				>
			</g>
			<g id="reserve tank">
				<rect
					id="Rectangle 38"
					x="450.5"
					y="456.5"
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
					><tspan x="470.666" y="490.364">&#x411;&#x430;&#x43a; &#x421;&#x412;&#x417;</tspan></text
				>
			</g>
			<g id="consumer">
				<rect
					id="Rectangle 38_2"
					x="566.5"
					y="39.5001"
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
					><tspan x="576.34" y="64.0304">&#x41f;&#x43e;&#x442;&#x440;. 1</tspan></text
				>

				<text
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="10"
					letter-spacing="0em"><tspan x="586.34" y="34.0304">{C1T}°C</tspan></text
				>
			</g>
			<g id="consumer_2">
				<rect
					id="Rectangle 38_3"
					x="564.5"
					y="111.5"
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
					><tspan x="573.496" y="136.031">&#x41f;&#x43e;&#x442;&#x440;. 2</tspan></text
				>
				<text
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="10"
					letter-spacing="0em"><tspan x="583.496" y="106.031">{C2T}°C</tspan></text
				>
			</g>
			<g id="consumer_3">
				<rect
					id="Rectangle 38_4"
					x="566.5"
					y="183.5"
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
					><tspan x="575.309" y="208.03">&#x41f;&#x43e;&#x442;&#x440;. 3</tspan></text
				>

				<text
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="10"
					letter-spacing="0em"><tspan x="585.309" y="178.03">{C3T}°C</tspan></text
				>
			</g>
			<g id="consumer_4">
				<rect
					id="Rectangle 38_5"
					x="566.5"
					y="255.5"
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
					><tspan x="575.28" y="280.03">&#x41f;&#x43e;&#x442;&#x440;. 4</tspan></text
				>
				<text
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="10"
					letter-spacing="0em"><tspan x="585.28" y="250.03">{C4T}°C</tspan></text
				>
			</g>
			<g id="consumer_5">
				<rect
					id="Rectangle 38_6"
					x="566.5"
					y="327.5"
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
					><tspan x="575.479" y="352.03">&#x41f;&#x43e;&#x442;&#x440;. 5</tspan></text
				>
				<text
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="10"
					letter-spacing="0em"><tspan x="585.479" y="322.03">{C5T}°C</tspan></text
				>
			</g>
			<g id="consumer_6">
				<rect
					id="Rectangle 38_7"
					x="566.5"
					y="399.5"
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
					><tspan x="575.385" y="424.03">&#x41f;&#x43e;&#x442;&#x440;. 6</tspan></text
				>
				<text
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="10"
					letter-spacing="0em"><tspan x="585.385" y="394.03">{C6T}°C</tspan></text
				>
			</g>
			<g
				id="Pump"
				class:hasError={CN1E}
				on:click={() => {
					if (CN1E) return;
					pump1Working ? (statePump1 = 'off') : (statePump1 = 'HS');
				}}
				on:contextmenu|preventDefault={() => (CN1E = !CN1E)}
				style="--fillColor: {signColor(pump1Working)}"
			>
				<path
					id="Ellipse 3"
					d="M139 13.5001C122.708 13.5001 109.5 26.7077 109.5 43.0001C109.5 59.2925 122.708 72.5001 139 72.5001C155.293 72.5001 168.5 59.2925 168.5 43.0001C168.5 26.7077 155.293 13.5001 139 13.5001Z"
					fill="var(--fillColor)"
					stroke="var(--strokeColor)"
					stroke-width="var(--strokeWidth)"
				/>
				<path
					id="Vector 19"
					d="M186 44.0001L167.5 50.5001C163.9 65.3001 150.667 71.0001 144.5 72.0001L186 72.0001L186 44.0001Z"
					fill="var(--fillColor)"
					stroke="var(--strokeColor)"
					stroke-width="var(--strokeWidth)"
				/>
				<path
					id="Vector 20"
					d="M95.0002 13.5001L138 13.5001C122 14.0001 112.834 26.5001 111.5 32.0001L95.0002 26.0001L95.0002 13.5001Z"
					fill="var(--fillColor)"
					stroke="var(--strokeColor)"
					stroke-width="var(--strokeWidth)"
				/>
				<text
					id="&#208;&#166;&#208;&#157; III-1"
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="12"
					letter-spacing="0em"><tspan x="95.0001" y="8.86376">&#x426;&#x41d; III-1</tspan></text
				>
			</g>
			<g
				id="Pump_2"
				class:hasError={CN2E}
				on:click={() => {
					if (CN2E) return;
					pump2Working ? (statePump2 = 'off') : (statePump2 = 'HS');
				}}
				on:contextmenu|preventDefault={() => (CN2E = !CN2E)}
				style="--fillColor: {signColor(pump2Working)}"
			>
				<path
					id="Ellipse 3_2"
					d="M136 114.5C119.708 114.5 106.5 127.708 106.5 144C106.5 160.292 119.708 173.5 136 173.5C152.293 173.5 165.5 160.292 165.5 144C165.5 127.708 152.293 114.5 136 114.5Z"
					fill="var(--fillColor)"
					stroke="var(--strokeColor)"
					stroke-width="var(--strokeWidth)"
				/>
				<path
					id="Vector 19_2"
					d="M183 145L164.5 151.5C160.9 166.3 147.667 172 141.5 173L183 173L183 145Z"
					fill="var(--fillColor)"
					stroke="var(--strokeColor)"
					stroke-width="var(--strokeWidth)"
				/>
				<path
					id="Vector 20_2"
					d="M92.0002 114.5L135 114.5C119 115 109.834 127.5 108.5 133L92.0002 127L92.0002 114.5Z"
					fill="var(--fillColor)"
					stroke="var(--strokeColor)"
					stroke-width="var(--strokeWidth)"
				/>
				<text
					id="&#208;&#166;&#208;&#157; III-1_2"
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="12"
					letter-spacing="0em"><tspan x="92.0001" y="109.864">&#x426;&#x41d; III-2</tspan></text
				>
			</g>
			<g
				id="Pump_3"
				class:hasError={CN3E}
				on:click={() => {
					if (CN3E) return;
					pump3Working ? (statePump3 = 'off') : (statePump3 = 'HS');
				}}
				on:contextmenu|preventDefault={() => (CN3E = !CN3E)}
				style="--fillColor: {signColor(pump3Working)}"
			>
				<path
					id="Ellipse 3_3"
					d="M139 215.5C122.708 215.5 109.5 228.708 109.5 245C109.5 261.292 122.708 274.5 139 274.5C155.293 274.5 168.5 261.292 168.5 245C168.5 228.708 155.293 215.5 139 215.5Z"
					fill="var(--fillColor)"
					stroke="var(--strokeColor)"
					stroke-width="var(--strokeWidth)"
				/>
				<path
					id="Vector 19_3"
					d="M186 246L167.5 252.5C163.9 267.3 150.667 273 144.5 274L186 274L186 246Z"
					fill="var(--fillColor)"
					stroke="var(--strokeColor)"
					stroke-width="var(--strokeWidth)"
				/>
				<path
					id="Vector 20_3"
					d="M95.0002 215.5L138 215.5C122 216 112.834 228.5 111.5 234L95.0002 228L95.0002 215.5Z"
					fill="var(--fillColor)"
					stroke="var(--strokeColor)"
					stroke-width="var(--strokeWidth)"
				/>
				<text
					id="&#208;&#166;&#208;&#157; III-1_3"
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="12"
					letter-spacing="0em"
					><tspan x="95.0001" y="210.864">&#x426;&#x41d; III-&#x420;</tspan></text
				>
			</g>
			<g id="valve_6" on:click={() => (v6 = !v6)}>
				<path
					id="Vector 21_6"
					d="M158 369V340L181.5 347.5V362L158 369Z"
					fill={signColor(v6)}
					stroke="black"
				/>
				<path
					id="Vector 22_6"
					d="M207.5 369V340L184 347.5V362L207.5 369Z"
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
					letter-spacing="0em"><tspan x="158" y="336.364">&#x41a;6</tspan></text
				>
			</g>
			<g id="valve_7" on:click={() => (v5 = !v5)}>
				<path
					id="Vector 21_7"
					d="M35.0002 469V440L58.5002 447.5V462L35.0002 469Z"
					fill={signColor(v5)}
					stroke="black"
				/>
				<path
					id="Vector 22_7"
					d="M84.5002 469V440L61.0002 447.5V462L84.5002 469Z"
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
					letter-spacing="0em"><tspan x="35.0002" y="436.364">&#x41a;5</tspan></text
				>
			</g>
			<g id="filter">
				<path
					id="Vector 21_8"
					d="M139 407.431L104 407.431L116.673 436L126.931 436L139 407.431Z"
					fill={signColor(filter)}
					stroke="black"
				/>
				<path
					id="Vector 22_8"
					d="M139 402.569L104 402.569L116.673 374L126.931 374L139 402.569Z"
					fill={signColor(filter)}
					stroke="black"
				/>
				<path id="Line 52" d="M103 405L139.5 405" stroke="black" stroke-dasharray="3 3" />
				<text
					id="Filter"
					fill="black"
					xml:space="preserve"
					style="white-space: pre"
					font-family="Inter"
					font-size="12"
					letter-spacing="0em"
					><tspan x="139" y="387.364">&#x424;&#x418;&#x41e; III&#x43a;</tspan></text
				>
			</g>
		</g>
	</svg>
</div>

<style>
	.container {
		display: grid;
		grid-template-columns: auto auto;
		column-gap: 32px;
	}

	.pumps-params {
		display: flex;
		flex-direction: column;
		row-gap: 16px;
	}
	#scheme {
		--strokeColor: black;
		--strokeWidth: 1;
	}
	.cooling-mode {
		margin-bottom: 16px;
	}
	.hasError {
		--strokeColor: rgb(255, 55, 55);
		--strokeWidth: 3;

		animation: blink 1s infinite;
	}
	#scheme-container {
		width: 100%;
	}

	@keyframes blink {
		50% {
			--strokeColor: black;
			--strokeWidth: 1;
		}
	}
</style>
