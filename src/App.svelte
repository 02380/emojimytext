<script>
	let input_text = '';

	$: input_text_emoji = input_text && create_new_txt('🅰🅱©∂📧🎏⛽♓ℹ🗾🎋👢Ⓜ♑⭕🅿Q®⚡🌴⛎♈📈❌✌Ⓩ')
	$: input_text_circled = input_text && create_new_txt('ⒶⒷⒸⒹⒺⒻⒼⒽⒾⒿⓀⓁⓂⓃⓄⓅⓆⓇⓈⓉⓊⓋⓌⓍⓎⓏ')
	$: input_text_fullwidth = input_text && create_new_txt('ＡＢＣＤＥＦＧＨＩＪＫＬＭＮＯＰＱＲＳＴＵＶＷＸＹＺ')
	$: input_text_blocks = input_text && create_new_txt('🅰🅱🅲🅳🅴🅵🅶🅷🅸🅹🅺🅻🅼🅽🅾🅿🆀🆁🆂🆃🆄🆅🆆🆇🆈🆉')
	$: input_text_doublestruck = input_text && create_new_txt('𝔸𝔹ℂ𝔻𝔼𝔽𝔾ℍ𝕀𝕁𝕂𝕃𝕄ℕ𝕆ℙℚℝ𝕊𝕋𝕌𝕍𝕎𝕏𝕐ℤ')
	$: input_text_backwards = input_text && create_new_txt('ɐqɔpǝɟƃɥıɾʞןɯuodbɹsʇn𐌡ʍxʎz')
	$: input_text_cjkt = input_text && create_new_txt('ﾑ乃cd乇ｷgんﾉﾌズﾚﾶ刀oｱq尺丂ｲu√wﾒﾘ乙')

	import {fade} from "svelte/transition"
	import emojiAware from "emoji-aware"

	let create_new_txt = (alef_replace) => {
		let loc_text = input_text.toUpperCase();
		let emojis = emojiAware.split(alef_replace);
		let alef = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('');
		for(let i = alef.length-1; i>=0; i--) {
			loc_text = loc_text.replaceAll(alef[i],emojis[i]);
		}
		return loc_text;
	}

</script>

<main in:fade>
	<h1>every text type ever - by <a href="http://github.com/02380">byron</a></h1>
	<input placeholder="start typing..." autofocus="autofocus" bind:value={input_text} type="text" name="this_doesnt_matter_but_ok">
	<h2>{input_text}</h2>
	<h2>{input_text_emoji}</h2>
	<h2>{input_text_circled}</h2>
	<h2>{input_text_fullwidth}</h2>
	<h2>{input_text_blocks}</h2>
	<h2>{input_text_backwards}</h2>
	<h2>{input_text_doublestruck}</h2>
	<h2>{input_text_cjkt}</h2>
</main>

<style>
	main {
		padding: 1em;
		padding-top: 0.2rem;
		/*max-width: 240px;*/
		margin: 0 auto;
	}
	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>