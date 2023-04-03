<script>
	let before = "";
	$: after = before
		.split("\n") // 改行で文章を分割
		.map((s) => s.replace(/^\s*\/\/\s*/, '')) // 各行の先頭が空白や 「//」 が含まれていたら削除
		.reduce((joined, current) => joined.slice(-1) == '.' ? `${joined}\n${current}` : `${joined} ${current}`);

	const clear = () => {
		before = "";
	}

	const copyToClipboard = async () => setTimeout(() => navigator.clipboard.writeText(after), 100);
</script>

<main>
	<h1>PHP のスラッシュで書かれた複数行コメントを<br/>いい感じに整形して翻訳しやすくするやつ</h1>
	<div style="margin-bottom: 40px;">
		<small style="display: block;">
			「//」で始まる複数行のコメントから，各行の先頭の 「//」 を除去します．
		</small>
		<small style="display: block;">
			また，文章がまだ続いている可能性が高い改行も削除します．
		</small>
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
