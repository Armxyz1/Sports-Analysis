<script lang="ts">
	import Sidebar from './components/sidebar.svelte';
    import Analytics from './shared/analytics.svelte';
	import Homepage from './shared/homepage.svelte';
	import Landing from './shared/Landing.svelte';
	import Team from './shared/Team.svelte';
	import Settings from './shared/settings.svelte';
	import { currentPage, pages } from './shared/progstate.svelte.ts';
	let socket:WebSocket;

	socket = new WebSocket("ws://localhost:8001/")
	socket.addEventListener('open',() => console.log("The websocket connection is successful"))
</script>

<svelte:head>
	<title>Project</title>
	<meta name="description" content="Football analysis" />
</svelte:head>

<div class="flex flex-row flex-grow items-stretch">
	<Sidebar />
	<div class="flex flex-col flex-grow" style="width: 100%;">
		<Landing visibility={$currentPage == pages.MAIN_HOME} />
		<Homepage {socket} visibility={$currentPage == pages.HOME} />
		<Analytics {socket} visibility={$currentPage == pages.ANALYTICS} />
		<Team visibility = {$currentPage == pages.TEAM} />
		<Settings visibility={$currentPage == pages.SETTINGS} />
	</div>
</div>

<style>
</style>
