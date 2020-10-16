<script>
	import {onMount} from "svelte";
	import {Router, Link, Route, navigate} from "svelte-routing"
	export let name = ""
	import TopAppBar, {Row, Section, Title, FixedAdjust, DenseFixedAdjust, ProminentFixedAdjust, ShortFixedAdjust} from '@smui/top-app-bar';
	import Drawer, {AppContent, Content, Header, Subtitle, Scrim} from '@smui/drawer';
	import List, {Item, Text, Graphic, Separator, Subheader} from '@smui/list';
	import H6 from '@smui/common/H6.svelte';
	import IconButton from '@smui/icon-button';
	import Landing from "./pages/Landing.svelte"
	import About from "./pages/About.svelte"
	let dense = false;
	let prominent = false;
	let Adjust = FixedAdjust;
	let title = "SMK"
	let fromChild;
	let myDrawer2;
	let menuOpen = false;
	let active_menu = 'Inbox';
	let variant = 'short';
	Adjust = ShortFixedAdjust;
	function routeNav(value,nav) {
		active_menu = value
		menuOpen = false;
		navigate(nav,{replace:false})
	}
	const bindData = async (n) => {
		fromChild = n;
	};

	onMount(()=>{
		title = fromChild.title;
	});
	console.log("Loaded")
	export let url;
</script>

<style>

</style>
<svelte:head>
	<title>{name}</title>
	<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
	<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,600,700">
	<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto+Mono">
</svelte:head>
<Drawer variant="dismissible"  bind:this={myDrawer2} bind:open={menuOpen}>
	<Header>
		<IconButton on:click={() => menuOpen = !menuOpen} class="material-icons">menu</IconButton>
	</Header>
	<Content>
		<List>
			<Item href="javascript:void(0)" on:click={() => routeNav('Beranda','/')} >
				<Graphic class="material-icons" aria-hidden="true">home</Graphic>
				<Text>Beranda</Text>
			</Item>
			<Item href="javascript:void(0)" on:click={() => routeNav('About','/about')} >
				<Graphic class="material-icons" aria-hidden="true">verified_user</Graphic>
				<Text>Tentang</Text>
			</Item>

		</List>
	</Content>
</Drawer>
<div class="top-app-bar-container flexor">
	<TopAppBar {variant} {prominent} {dense} color='primary'>
		<Row>
			<Section>
				<IconButton on:click={() => menuOpen = !menuOpen} class="material-icons">menu</IconButton>
				<Title>{title}</Title>
			</Section>
		</Row>
	</TopAppBar>
	<div use:Adjust>
		<Router url="{url}">
			<div>
				<Route path="/" component="{Landing}" bindData={bindData} />
				<Route path="/about" component="{About}" bindData={bindData} />
			</div>
		</Router>
	</div>
</div>
