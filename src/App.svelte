<script>
	import {fade} from "svelte/transition"
	import emojiAware from "emoji-aware"

	let input_text = '';

	$: input_text_emoji = input_text && create_new_txt('🅰🅱©Ⓓ📧🎏⛽♓ℹ🗾🎋👢Ⓜ♑⭕🅿Ⓠ®⚡🌴⛎♈📈❌✌Ⓩ')
	$: input_text_emoji_special = input_text && create_new_specialmoji();
	$: input_text_circled = input_text && create_new_txt('ⒶⒷⒸⒹⒺⒻⒼⒽⒾⒿⓀⓁⓂⓃⓄⓅⓆⓇⓈⓉⓊⓋⓌⓍⓎⓏ')
	$: input_text_fullwidth = input_text && create_new_txt('ＡＢＣＤＥＦＧＨＩＪＫＬＭＮＯＰＱＲＳＴＵＶＷＸＹＺ')
	$: input_text_blocks = input_text && create_new_txt('🅰🅱🅲🅳🅴🅵🅶🅷🅸🅹🅺🅻🅼🅽🅾🅿🆀🆁🆂🆃🆄🆅🆆🆇🆈🆉')
	$: input_text_doublestruck = input_text && create_new_txt('𝔸𝔹ℂ𝔻𝔼𝔽𝔾ℍ𝕀𝕁𝕂𝕃𝕄ℕ𝕆ℙℚℝ𝕊𝕋𝕌𝕍𝕎𝕏𝕐ℤ')
	$: input_text_backwards = input_text && create_new_txt('ɐqɔpǝɟƃɥıɾʞןɯuodbɹsʇn𐌡ʍxʎz')
	$: input_text_cjkt = input_text && create_new_txt('ﾑ乃cd乇ｷgんﾉﾌズﾚﾶ刀oｱq尺丂ｲu√wﾒﾘ乙')


	let create_new_specialmoji = (alef_replace) => {
		let special_cases = [['be','🐝'],['end','🔚'],['abc','🔤'],['world','🌎'],
			['car','🚙'],['ok','🆗'],['cool','🆒'],['cl','🆑'],
			['id','🆔'],['sos','🆘'],['atm','🏧'],['new','🆕'],['ng','🆖'],['soon','🔜'],['free','🆓']];
		let punmoji = false, loc_text = input_text;
		special_cases.forEach((sc) => {
			console.log(input_text.search(sc[0]));
			if (input_text.search(sc[0]) !== -1	) {
				loc_text = loc_text.replaceAll(sc[0],sc[1]);
				punmoji = true;
			}
		});
		if (punmoji == true) {
			return create_new_txt_long('🅰🅱©∂📧🎏⛽♓ℹ🗾🎋👢Ⓜ♑⭕🅿Q®⚡🌴⛎♈📈❌✌Ⓩ',loc_text);
		} else {
			return undefined;
		}
	}

	let create_new_txt = (alef_replace) => {
		return create_new_txt_long(alef_replace, input_text)
	}

	let create_new_txt_long = (alef_replace, strb) => {
		let loc_text = strb.toUpperCase();
		let emojis = emojiAware.split(alef_replace);
		let alef = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('');
		for(let i = alef.length-1; i>=0; i--) {
			loc_text = loc_text.replaceAll(alef[i],emojis[i]);
		}
		return loc_text;
	}
	if (!String.prototype.replaceAll) {
	  String.prototype.replaceAll = function(find, replace) {
	    let s = '', index, next;
	    while (~(next = this.indexOf(find, index))) {
	      s += this.substring(index, next) + replace;
	      index = next + find.length;
	    }
	    return s + this.substring(index);
	  };
	}
</script>

<main in:fade>
	<h1>every text type ever - by <a href="http://github.com/02380">byron</a></h1>
	<input placeholder="start typing..." autofocus="autofocus" bind:value={input_text} type="text" name="this_doesnt_matter_but_ok">
	{#if input_text}<div class="text"><small>Text</small><h2>{input_text}</h2></div>{/if}
	{#if input_text_emoji}<div class="text"><small>emoji</small><h2>{input_text_emoji}</h2></div>{/if}
	{#if input_text_emoji_special}<div class="text"><small>punemoji</small><h2>{input_text_emoji_special}</h2></div>{/if}
	{#if input_text_circled}<div class="text"><small>circle</small><h2>{input_text_circled}</h2></div>{/if}
	{#if input_text_fullwidth}<div class="text"><small>fullwidth</small><h2>{input_text_fullwidth}</h2></div>{/if}
	{#if input_text_blocks}<div class="text"><small>blocks</small><h2>{input_text_blocks}</h2></div>{/if}
	{#if input_text_backwards}<div class="text"><small>backwards</small><h2>{input_text_backwards}</h2></div>{/if}
	{#if input_text_doublestruck}<div class="text"><small>math doublestruck</small><h2>{input_text_doublestruck}</h2></div>{/if}
	{#if input_text_cjkt}<div class="text"><small>CJK+thai</small><h2>{input_text_cjkt}</h2></div>{/if}
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