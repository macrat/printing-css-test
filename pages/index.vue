<style scope>
@page :first {
	margin-top: 0;
}
@page {
	size: a4;
	margin: 17mm 0;
}

body {
	margin: 0;
	background-color: white;
}

header {
	position: fixed;
	top: 0;
	left: 0;
	right: 0;
	padding: .2em .5em;
	height: 1em;

	background-color: black;
	font-size: 170%;
}
header text {
	fill: white;
	dominant-baseline: text-before-edge;
}
#header--print-information {
	display: none;
}

main {
	margin: 3.5em 5em 1em;
}

main p {
	orphans: 100;
	widows: 100;
}

@media print {
	header {
		position: absolute;
		padding: 2mm;
		height: 2.5cm;

		background-color: transparent;
	}
	header::after {
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		content: ' ';
		border-top: 3cm solid black;
		z-index: -10;
	}
	#header--site-name {
		position: absolute;
		width: 100%;
		position: absolute;
		top: 0;
	}
	#header--site-name text {
		font-size: 3.5cm;
		text-transform: capitalize;
		font-variant: small-caps;
		font-family: "impact", fantacy, sans-serif;

		background-color: none;
	}
	#header--print-information {
		display: flex;
		float: right;
		flex-direction: column;
		align-items: flex-end;

		font-size: 4mm;
	}
	#header--print-information img {
		width: 2cm;
		height: 2cm;
	}
	main {
		margin: 3.5cm 15mm 0;
		font-family: Georgia, "Times New Roman", Times, serif;
	}

	p {
		margin: 2mm 0;
		line-height: 1.3;
	}
	p::first-letter {
		font-size: 240%;
		line-height: 1;
		margin-right: 2mm;
		float: left;
	}
}
</style>

<template>
	<div id=app>
		<header>
			<svg id=header--site-name><text text-anchor="start">site name</text></svg>

			<div id=header--print-information>
				<svg id=header--url height=1em width="400px"><text x="400" text-anchor="end">{{ url }}</text></svg>
				<img :src=qrcode />
			</div>
		</header>

		<main>
			<h1>this is content</h1>
			<p v-for="_ in Array.from({length:5})">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
			<h1>日本語のコンテンツ</h1>
			<p v-for="_ in Array.from({length:5})">吾輩は猫である。名前はまだ無い。どこで生れたかとんと見当がつかぬ。何でも薄暗いじめじめした所でニャーニャー泣いていた事だけは記憶している。吾輩はここで始めて人間というものを見た。しかもあとで聞くとそれは書生という人間中で一番獰悪な種族であったそうだ。この書生というのは時々我々を捕つかまえて煮にて食うという話である。しかしその当時は何という考もなかったから別段恐しいとも思わなかった。ただ彼の掌に載せられてスーと持ち上げられた時何だかフワフワした感じがあったばかりである。掌の上で少し落ちついて書生の顔を見たのがいわゆる人間というものの見始みはじめであろう。</p>
		</main>
	</div>
</template>

<script>
import QRCode from 'qrcode';

export default {
	data: () => ({
		url: '',
		qrcode: '',
	}),
	mounted() {
		this.url = location.href;
		QRCode.toDataURL(location.href, {color: {light: '#00000000', dark: '#ffffffff'}})
			.then(url => this.qrcode = url);
	},
}
</script>
