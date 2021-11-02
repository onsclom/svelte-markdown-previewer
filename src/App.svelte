<script>
	import markdown from 'marked'
	import EyeIcon from '@svelte-parts/icons/feather/eye'
	import PenIcon from '@svelte-parts/icons/feather/pen-tool'
	let name = 'world';
	let markdownText = `# Welcome to my Svelte Markdown Previewer!

## This is a sub-heading...
### And here's some other cool stuff:
  
Heres some code, \`<div></div>\`, between 2 backticks.

\`\`\`
// this is multi-line code:

function anotherExample(firstLine, lastLine) {
  if (firstLine == '\`\`\`' && lastLine == '\`\`\`') {
    return multiLineCode;
  }
}
\`\`\`
  
You can also make text **bold**... whoa!
Or _italic_.
Or... wait for it... **_both!_**
And feel free to go crazy ~~crossing stuff out~~.

There's also [links](https://www.freecodecamp.com), and
> Block Quotes!

And if you want to get really crazy, even tables:

Wild Header | Crazy Header | Another Header?
------------ | ------------- | ------------- 
Your content can | be here, and it | can be here....
And here. | Okay. | I think we get it.

- And of course there are lists.
  - Some are bulleted.
     - With different indentation levels.
        - That look like this.


1. And there are numbered lists too.
1. Use just 1s if you want! 
1. But the list goes on...
- Even if you use dashes or asterisks.
* And last but not least, let's not forget embedded images:

![Svelte Logo](https://subscribe.packtpub.com/wp-content/uploads/2020/10/svelte_js.png)`

	$: output = markdown(markdownText)

	let curFocus = "neither"
	function chooseFocus(side) {
		console.log(side)
		if (curFocus == "neither") {
			curFocus = side
		} else {
			curFocus = "neither"
		}
	}
</script>

<main>
	<div class="container" class:shrink="{curFocus === 'right'}" >
		<span class="header" on:click={()=>{chooseFocus("left")}}>markdown <PenIcon></PenIcon></span>
		<textarea bind:value={markdownText} id="editor"></textarea>
	</div>
	<div class="container" class:shrink="{curFocus === 'left'}">
		<span class="header" on:click={()=>{chooseFocus('right')}}>preview <EyeIcon></EyeIcon></span>
		<div id="preview">
			{@html output}
		</div>
	</div>
	<!-- <div class="half-panel">
	</div>
	<div class="half-panel">
	</div> -->
</main>

<style>

	#preview {
		border: 2px solid black;
		border-radius: 0rem .5rem .5rem .5rem;
		background: white;
		padding: 1rem;
		overflow: scroll;
	}

	.header {
		/* position: fixed; */
		padding: .4rem;
		font-size: 1.5rem;
		text-align: center;
		border: 2px solid black;
		border-bottom: 0;
		align-self:flex-start;
		background: white;
		border-radius: .5rem .5rem 0 0;
		transform: translate(0,2px);
		cursor: pointer;
	}

	.container {
		margin: .5rem;
		display: flex;
		flex-direction: column;
		box-sizing: content-box;
		flex-basis: 0;

		/* box-shadow: 4px 4px 0px 0px #000000; */
		-moz-transition: ease-in-out all 0.3s 0s;
    -o-transition: ease-in-out all 0.3s 0s;
    -webkit-transition: ease-in-out all 0.3s 0s;
		transition: ease-in-out all 0.3s 0s;

		max-width: 40rem;
	}
	
	main {
		height: 100%;
		width: 100%;
		margin: auto;
		display: flex;
		justify-content: center
	}
	
	@media (max-width: 600px) {
		main {
			flex-direction: column;
		}
	}
	
	textarea {
		border: 2px solid black;
		border-radius: 0rem .5rem .5rem .5rem;
		margin:0;
		padding:0;
		display: block;
		resize: none;
		outline: none;
		font-size: 1rem;
		font-family: monospace;
		display: flex;
		flex-grow: 1;
		padding: 1rem;
	}
	div {
		flex-grow: 1;
		overflow: hidden;
	}
	
	.shrink {
		flex-grow: 0;
	}
</style>