<script>
	import { onMount, onDestroy } from "svelte";
	import TypeWriter from "./TypeWriter.svelte";
	let colors = [
		"#BE00FF",
		"#00FEFF",
		"#FF8300",
		"#0026FF",
		"#FFFA01",
		"#FF2600",
		"#FF008B",
	];
	let number = 0;
	let logoSize = 180;
	let logoColor = "#FFFFFF";
	let windowHeight;
	let windowWidth;
	let xPosition = 0;
	let xDirection = 3;
	let yPosition = 0;
	let yDirection = 3;

	let intervalId;
	onMount(() => {
		intervalId = setInterval(() => {
			xPosition += xDirection;
			if (xPosition + 200 > windowWidth || xPosition < 0) {
				changeColor();
				xDirection *= -1;
			}
			yPosition += yDirection;
			if (yPosition + 200 > windowHeight || yPosition < 0) {
				changeColor();
				yDirection *= -1;
			}
		}, 20);
		console.log(windowHeight, windowWidth);
	});

	onDestroy(() => {
		clearInterval(intervalId);
	});

	function changeColor() {
		if (number == colors.length - 1) {
			number = 0;
		} else {
			number++;
		}
		logoColor = colors[number];
	}
</script>

<!-- This looks super odd on mobile for some reason, but I will accept it because I like how it looks -->
<body class="h-screen w-screen">
	<h1
		class="text-white flex items-center justify-center text-6xl w-screen h-screen"
	>
		<TypeWriter
			words={[
				"*Despite everything, it's still you.",
				"Click the logo to go home.",
			]}
		/>
	</h1>
	<a href="/">
		<svg
			width={logoSize}
			viewBox="0 0 2400 2400"
			preserveAspectRatio="xMidYMid meet"
			style="position: absolute; left: {xPosition}px; top: {yPosition}px"
		>
			<g
				transform="translate(0.000000,2400.000000) scale(0.100000,-0.100000)"
				fill={logoColor}
				stroke="none"
			>
				<path
					d="M6565 15083 c7 -3226 6 -3503 -9 -3562 -71 -277 -333 -456 -613 -421 -217 28 -391 173 -466 390 l-22 65 -3 1238 -3 1237 -1695 0 -1695 0 4 -1397 c4 -1522 1 -1452 62 -1788 171 -941 676 -1783 1430 -2384 546 -436 1191 -715 1885 -817 608 -89 1413 -31 2070 148 1109 303 1935 924 2397 1803 l63 120 0 -2147 0 -2148 1605 0 1605 0 0 3423 c0 2978 2 3430 15 3484 48 204 213 374 415 428 71 19 220 19 293 0 112 -29 222 -100 300 -195 47 -56 102 -168 116 -238 8 -38 11 -706 11 -2292 l0 -2240 1600 0 c880 0 1600 1 1601 3 0 1 7 1001 14 2223 15 2464 9 2272 82 2421 41 85 130 186 210 239 31 21 93 50 137 66 69 24 97 28 186 28 90 0 117 -4 187 -29 176 -61 298 -185 365 -371 l23 -65 3 -2257 2 -2258 1600 0 1600 0 -3 3343 -2 3342 -23 98 c-92 399 -286 739 -608 1062 -575 577 -1512 1003 -2486 1129 -340 44 -752 53 -1043 22 -743 -80 -1340 -338 -1754 -760 l-64 -65 -86 86 c-181 181 -364 310 -616 433 -401 197 -794 291 -1337 321 -628 34 -1378 -95 -2013 -346 -165 -65 -495 -228 -640 -315 -517 -313 -901 -703 -1105 -1125 -93 -192 -138 -336 -171 -545 -17 -112 -17 -61 -18 1998 l-1 2112 -1706 0 -1706 0 7 -3497z"
				/>
			</g>
		</svg>
	</a>
</body>

<svelte:window bind:innerHeight={windowHeight} bind:innerWidth={windowWidth} />

<style>
	/* Interesting, actually. 404 Pages automatically wrapped inside of a body tag. I suppose that makes sense, though... */
	body {
		@apply m-0 bg-black p-0;
	}
</style>
