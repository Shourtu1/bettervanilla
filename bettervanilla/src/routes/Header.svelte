<script lang="js">
	const storageKey = 'theme-preference';
	import { onMount } from 'svelte';

	var themeTitle = 'Theme';

	onMount(() => {
		setthemePreference();
		if (document.documentElement.getAttribute('data-theme') === 'dark') {
			themeTitle = 'Theme🌙';
		} else if (document.documentElement.getAttribute('data-theme') === 'light') {
			themeTitle = 'Theme☀️';
		}
	});

	// using click functions to close theme switcher for mobile devices compatibility
	function themeswitcherCloseAuto() {
		themeSwitcherClose();
		setthemeAuto();
		setPreference();
	}

	function themeswitcherCloseDark() {
		themeSwitcherClose();
		setthemeDark();
		setPreference();
	}

	function themeswitcherCloseLight() {
		themeSwitcherClose();
		setthemeLight();
		setPreference();
	}

	// main switcher functions
	function themeSwitcherClose() {
		document.getElementById('themeSelector').removeAttribute('open');
	}

	function getPreference() {
		return document.documentElement.getAttribute('data-theme');
	}

	function setPreference() {
		localStorage.setItem(storageKey, getPreference());
	}

	function setthemePreference() {
		if (localStorage.getItem(storageKey)) {
			document.documentElement.setAttribute('data-theme', localStorage.getItem(storageKey));
			if (localStorage.getItem(storageKey) === 'dark') {
				themeTitle = 'Theme🌙';
			} else if (localStorage.getItem(storageKey) === 'light') {
				themeTitle = 'Theme☀️';
			} else {
				themeTitle = 'Theme';
			}
		} else {
			setthemeAuto();
		}
	}

	function setthemeAuto() {
		document.documentElement.setAttribute('data-theme', 'auto');
		themeTitle = 'Theme';
	}

	function setthemeDark() {
		document.documentElement.setAttribute('data-theme', 'dark');
		themeTitle = 'Theme🌙';
	}

	function setthemeLight() {
		document.documentElement.setAttribute('data-theme', 'light');
		themeTitle = 'Theme☀️';
	}
</script>

<div
	style="-webkit-backdrop-filter: blur(20px); z-index: 99; position: fixed; right: 0; left: 0; backdrop-filter: blur(20px);"
>
	<nav class="container-fluid" style="box-shadow: 0 1px 0 rgba(115, 130, 140, 0.2);">
		<ul>
			<li><a href="/"><strong>BetterVanilla✨</strong></a></li>
		</ul>
		<ul>
			<li>
				<details role="list" dir="rtl" id="themeSelector">
					<summary aria-haspopup="listbox" role="link">{themeTitle}</summary>
					<ul role="listbox">
						<!-- svelte-ignore a11y-mouse-events-have-key-events -->
						<li>
							<a
								href={'#'}
								on:mouseover={setthemeAuto}
								on:mouseleave={setthemePreference}
								on:click={themeswitcherCloseAuto}>Auto</a
							>
						</li>
						<!-- svelte-ignore a11y-mouse-events-have-key-events -->
						<li>
							<a
								href={'#'}
								on:mouseover={setthemeDark}
								on:mouseleave={setthemePreference}
								on:click={themeswitcherCloseDark}>Dark</a
							>
						</li>
						<!-- svelte-ignore a11y-mouse-events-have-key-events -->
						<li>
							<a
								href={'#'}
								on:mouseover={setthemeLight}
								on:mouseleave={setthemePreference}
								on:click={themeswitcherCloseLight}>Light</a
							>
						</li>
					</ul>
				</details>
			</li>
			<li>
				<a href="/docs">Docs</a>
			</li>
			<li>
				<a href="/downloads">Downloads</a>
			</li>
			<li><a href="/info">Info</a></li>
		</ul>
	</nav>
</div>
