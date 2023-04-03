<script>
	let type = "double-slash";

	let before = "";
	$: after = before
		.split("\n") // 改行で文章を分割
		.map((s) => converters[type](s)) // 各行の先頭が空白や 「//」 が含まれていたら削除
		.reduce((joined, current) => joined.slice(-1) == '.' ? `${joined}\n${current}` : `${joined} ${current}`);

	const converters = {
		"double-slash": (s) => s.replace(/^\s*\/\/\s*/, ''),
		"slash-asterisk": (s) => s.replace(/^\s*(\/\*\*|\/\*|\*\/|\*\*\/|\*)\s*/, ''),
		"hash": (s) => s.replace(/^\s*#\s*/, ''),
		"empty": (s) => s.replace(/^\s+/, ''),
	};


	// クリア
	const clear = () => { before = ""; };

	// クリップボードにコピー
	const copyToClipboard = async () => setTimeout(() => navigator.clipboard.writeText(after), 100);
</script>

<main>
	<h1>複数行コメントをいい感じに整形して<br/>翻訳しやすくするやつ</h1>
	<div style="margin-bottom: 40px;">
		<small style="display: block;">
			「/*」や 「//」などで書かれた複数行コメントをただの文章に変換します．
		</small>
		<small style="display: block;">
			これにより, DeepL などの翻訳へのコピペが楽になります．
		</small>
	</div>

	<div style="text-align: start; width: fit-content; margin: auto; margin-bottom: 40px; ">
		<label>
			<input type="radio" bind:group={type} name="comment-type" value={"double-slash"}>
			「//」ではじまるもの
		</label>
		<label>
			<input type="radio" bind:group={type} name="comment-type" value={"hash"}>
			「#」ではじまるもの
		</label>
		<label>
			<input type="radio" bind:group={type} name="comment-type" value={"slash-asterisk"}>
			「/*」や「/**」ではじまり，「*/」や「**/」で終わるもの
		</label>
		<label>
			<input type="radio" bind:group={type} name="comment-type" value={"empty"}>
			各行先頭が空白
		</label>
	</div>

	<div class="app-area">
		<textarea
			name="before"
			id="before"
			cols="50"
			rows="10"
			bind:value={before}
		></textarea>

		<div>
			<button on:click={() => clear()}>クリア</button>
		</div>

		<p style="font-size: 40px;">🔽</p>

		<textarea
			name="after"
			id="after"
			cols="50"
			rows="10"
			bind:value={after}
			readonly
		></textarea>

		<div>
			<button on:click={() => copyToClipboard()}>📋 クリップボードにコピー</button>
		</div>
	</div>

</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		min-width: 640px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
