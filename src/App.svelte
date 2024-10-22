<!-- Scriptabschnitt im die Logik der Website zu Erzeugen -->
<script>
	// Begriffe welche in gendergerechte Sprache übersetzt werden
	const replacements = [
		{ from: /\bStudenten\b/gi, to: 'Student:innen', word: 'Studenten' },
		{ from: /\bStudent\b/gi, to: 'Student:innen', word: 'Student' },
		{ from: /\bLehrer\b/gi, to: 'Lehrkräfte', word: 'Lehrer' },
		{ from: /\bArzt\b/gi, to: 'Ärztin/Arzt', word: 'Arzt' },
		{ from: /\bPatient\b/gi, to: 'Patientin/Patient', word: 'Patient' },
		{ from: /\bSchüler\b/gi, to: 'Schülerinnen und Schüler', word: 'Schüler' },
		{ from: /\bMitarbeiter\b/gi, to: 'Mitarbeitender', word: 'Mitarbeiter' },
		{ from: /\bKollegen\b/gi, to: 'Kolleg:innen', word: 'Kollegen' },
	];

	let inputText = '';
	let transformedText = '';

	function transformText() {
		let newText = inputText;
		replacements.forEach(({ from, to }) => {
			newText = newText.replace(from, to);
		});
		transformedText = gender(newText);
	}

	function gender(text) {
		const div = document.createElement('div');
		div.textContent = text;
		return div.innerHTML;
	}

</script>

<!-- definieren der Klassen und deren Design´s -->
<style>
	:global(html, body) {
		height: 100%;
		margin: 0;
		padding: 0;
	}

	:global(body) {
		background-image: url('background.jpg');
		background-size: cover;
		background-position: center;
		background-repeat: no-repeat;
	}

	.container {
		min-height: 100vh;
		display: flex;
		flex-direction: column;
	}

	.menu{
		display: flex;
		justify-content: center;
		margin-top: 20px;
	}

	.section {
		flex: 1;
	}

	.content-container {
		padding: 20px;
		margin: 0 auto;
		max-width: 800px;
		color: white;
		text-shadow: 1px 1px 2px #000;
	}

	.has-text-centered {
		text-align: center;
	}

	.textarea {
		width: 100%;
		min-height: 200px;
		margin-bottom: 20px;
		color: white;
	}

	label.label {
		color: #fff;
	}

	.button.is-primary {
		background-color: #3273dc;
		color: #fff;
	}

	.transformed-text {
		color: #fff !important;
		text-shadow: 1px 1px 2px #000;
	}

	.footer {
		background-color: transparent !important;
		margin-top: auto;
	}

	.footer .content {
		color: #fff;
	}

	.footer a {
		color: #fff;
	}
</style>


<!-- Erzeugen des Headers und der Menülinks (diese sind ohne Funktion) -->
<div class="container">
	<section class="section">
		<div class="content has-text-centered">
			<h1 class="title" style="color: #fff; text-shadow: 1px 1px 2px #000;">Gender Automat</h1>
			<div class="menu" style="color: white">
				<a href="#" style="margin: 0 30px; color: beige; text-decoration: underline; font-weight: bold; text-shadow: 1px 1px 2px #000;">Menüpunkt 1</a>
				<a href="#" style="margin: 0 30px; color: beige; text-decoration: underline; font-weight: bold; text-shadow: 1px 1px 2px #000;">Menüpunkt 2</a>
				<a href="#" style="margin: 0 30px; color: beige; text-decoration: underline; font-weight: bold; text-shadow: 1px 1px 2px #000;">Menüpunkt 3</a>
			</div>
			<figure class="image is-128x128 is-inline-block">
				<img src="logo_new.png" alt="Logo">
			</figure>
		</div>
	</section>

	<!-- Sektion mit Textbox zur Eingabe eines Textes welcher gegendert werden soll -->
	<section class="section">
		<div class="content-container has-text-centered">
			<div class="field">
				<label class="label" style="color: white; text-shadow: 1px 1px 2px #000;">Bitte geben Sie Ihren Text ein:</label>
				<div class="control">
          <textarea
				  class="textarea"
				  bind:value={inputText}
				  placeholder="Hier Ihren Text eingeben..."
		  ></textarea>
				</div>
			</div>

			<div class="field is-grouped is-grouped-centered">
				<div class="control">
					<button class="button is-primary" on:click={transformText}>Text anpassen</button>
				</div>
			</div>

			<!-- Ausgabe des transformierten Textes -->
			{#if transformedText}
				<div class="content has-text-centered"
					style="margin-top: 30px; color: #fff;">
					<h2
							class="subtitle"
							style="color: #fff; text-shadow: 1px 1px 2px #000;"
					>
						Angepasster Text:
					</h2>
					<p class="transformed-text">{@html transformedText}</p>
				</div>
			{/if}

			<!-- Auflistung der verfügbaren Begriffe um die Demo der Website etwas zu vereinfachen -->
			<div
					class="content has-text-centered"
					style="margin-top: 50px; margin-bottom: 70px;"
			>
				<h2
						class="subtitle"
						style="color: #fff; text-shadow: 1px 1px 2px #000;"
				>
					Verfügbare Begriffe zur Anpassung
				</h2>
				<h5
					class="subtitle"
					style="color: #fff; text-shadow: 1px 1px 2px #000;"
					>
					Die Begriffe werden stetig ergänzt!
				</h5>
				<ul style="display: inline-block; text-align: left; color: #fff;">
					{#each replacements as item}
						<li>{item.word} &rarr; {item.to}</li>
					{/each}
				</ul>
			</div>
		</div>
	</section>

	<!-- Footerbereich mit kurzer Angabe zum Autor bzw. Zweck der Website -->
	<footer class="footer">
		<div class="content has-text-centered">
			<p>
				&copy; 2024 Felix Hagen. Im Auftrag der IU - Internatione Hochschule
			</p>
		</div>
	</footer>
</div>
