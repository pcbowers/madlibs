<script>
	import { fade } from "svelte/transition";

	let done = false;
	let index = 0;
	let opposite = "John";
	let button_val = "";

	let options = [
		["1. Verb (Past Tense)", ""],
		["2. Place (Proper Noun)", ""],
		["3. Transportation", ""],
		["4. Adjective", ""],
		["5. Adjective", ""],
		["6. John / Danica", ""],
		["7. Verb", ""],
		["8. Feeling (Adjective, he is feeling ___)", ""],
		["9. Verb", ""],
		["10. Verb", ""],
		["11. Advice (Start with Verb/Adverb)", ""],
		["12. Number", ""],
		["13. Adjective", ""],
		["14. Feeling (Noun, ___ is a feeling)", ""],
		["15. Name of Party Guest", ""],
	];

	$: {
		done = options.every((item, i) => {
			if (i === 5)
				opposite = item[1].toLowerCase() === "john" ? "Danica" : "John";

			if (item[1] === "") {
				index = i;
				return false;
			} else {
				return true;
			}
		});
	}

	function handleSubmit() {
		options[index][1] = button_val;
		button_val = "";
	}

	function handleEnter(e) {
		if (!e) e = window.event;
		var keyCode = e.code || e.key;
		if (keyCode === "Enter") {
			handleSubmit();
		}
	}

	function capitalizeFirstLetter(string) {
		return string.charAt(0).toUpperCase() + string.slice(1).toLowerCase();
	}
</script>

<main>
	{#if !done}
		{#each [options[index][0]] as choice (choice)}
			<section id="test" in:fade={{ delay: 500 }} out:fade>
				<div class="form__group field">
					<input
						type="input"
						class="form__field"
						placeholder={choice}
						name="name"
						id="name"
						required
						bind:value={button_val}
						on:keypress={handleEnter}
					/>
					<label for="name" class="form__label">{choice}</label>
				</div>
			</section>
		{/each}
	{:else}
		<section in:fade={{ delay: 500 }} out:fade>
			<h1>Dear John and Danica,</h1>
			<p>
				When I found out you guys were getting married, I <strong
					>{options[0][1].toLowerCase()}</strong
				>! I just knew I couldn't miss out, so I travelled all the way from
				<strong>{options[1][1].toLowerCase()}</strong>
				via a
				<strong>{options[2][1].toLowerCase()}</strong> to attend your
				<strong>{options[3][1].toLowerCase()}</strong>
				engagment party. I'm so excited that I was invited to this
				<strong>{options[4][1].toLowerCase()}</strong> party, especially as you begin
				your lives together.
			</p>
			<p>
				First of all, <strong>{capitalizeFirstLetter(options[5][1])}</strong>,
				you should never
				<strong>{options[6][1].toLowerCase()}</strong>
				no matter how
				<strong>{options[7][1].toLowerCase()}</strong>
				<strong>{capitalizeFirstLetter(opposite)}</strong>
				makes you, and
				<strong>{capitalizeFirstLetter(opposite)}</strong>, don't forget to
				<strong>{options[8][1].toLowerCase()}</strong>
				when you
				<strong>{options[9][1].toLowerCase()}</strong>. But most of all, you
				should both always
				<strong>{options[10][1].toLowerCase()}</strong>.
			</p>
			<p>
				Here's to wishing you <strong>{options[11][1]}</strong> years of a
				<strong>{options[12][1].toLowerCase()}</strong>
				marriage and even more years of
				<strong>{options[13][1].toLowerCase()}</strong>.
			</p>
			<p>
				Love,<br />
				<strong>{capitalizeFirstLetter(options[14][1])}</strong>
			</p>
		</section>
	{/if}
</main>

<style>
	main {
		text-align: center;
		max-width: 600px;
		margin: 0 auto;
	}

	#test {
		position: absolute;
		left: 50%;
		top: 50%;
		width: 90%;
		transform: translate(-50%, -50%);
	}

	.form__group {
		position: relative;
		padding: 15px 0 0;
		margin-top: 10px;
		width: 100%;
	}

	.form__field {
		font-family: inherit;
		width: 100%;
		border: 0;
		border-bottom: 2px solid #9b9b9b;
		outline: 0;
		font-size: 1.3rem;
		color: #fff;
		padding: 7px 0;
		background: transparent;
		transition: border-color 0.2s;
	}
	.form__field::placeholder {
		color: transparent;
	}
	.form__field:placeholder-shown ~ .form__label {
		font-size: 1.3rem;
		cursor: text;
		top: 20px;
	}

	.form__label {
		position: absolute;
		top: 0;
		display: block;
		transition: 0.2s;
		font-size: 1rem;
		color: #9b9b9b;
	}

	.form__field:focus {
		padding-bottom: 6px;
		font-weight: 700;
		border-width: 3px;
		border-image: linear-gradient(to right, #11998e, #38ef7d);
		border-image-slice: 1;
	}
	.form__field:focus ~ .form__label {
		position: absolute;
		top: 0;
		display: block;
		transition: 0.2s;
		font-size: 1rem;
		color: #11998e;
		font-weight: 700;
	}

	/* reset input */
	.form__field:required,
	.form__field:invalid {
		box-shadow: none;
	}

	strong {
		color: #11998e;
	}

	section {
		font-size: 1em;
		font-weight: 100;
		color: #fff;
	}

	@media (max-width: 600px) {
		main {
			max-width: none;
		}
	}

	h1 {
		font-size: 1.5em;
		font-weight: 100;
		color: #fff;
	}
</style>
