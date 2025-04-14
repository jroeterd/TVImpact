<script>
	import '@evidence-dev/tailwind/fonts.css';
	import '../app.css';
	import { EvidenceDefaultLayout } from '@evidence-dev/core-components';
	export let data;
</script>

<EvidenceDefaultLayout {data} 
	logo="logo.png"
	fullWidth=true
	neverShowQueries=true
	githubRepo="https://github.com/jroeterd/tvimpact"
	hideTOC=true
	>
	<slot slot="content" />
</EvidenceDefaultLayout>
