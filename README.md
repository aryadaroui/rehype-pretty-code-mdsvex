# Rehype Pretty Code MDsveX

This is a straight fork of [rehype pretty code](https://rehype-pretty-code.netlify.app/), except it can be used more readily with MDsveX. 

Currently, rehype-pretty-code works for code blocks in MDsveX, but the inline language syntax highlighting features don't work because of how MDsveX has to handle Svelte's curly brackets.

To use, you can follow all of the documentation expected with rehype-pretty-code and MDsveX, BUT, you must disable MDsveX's highlighter. Otherwise, the highlighter will overwrite your rehype-pretty-code formatting.

Example config:

with expected MDsveX config:
```javascript
// mdsvex.config.js

// ...

 const config = defineConfig({
	extensions: ['.svelte.md', '.md', '.svx'],

	smartypants: {
	},

	remarkPlugins: [remarkMath],
	rehypePlugins: [[rehypePrettyCode, prettyCodeOptions], addCustomAttribute, rehypeKatex, is_it_working],

	highlight: false, // this is important! will otherwise overwrite your rehype-pretty-code highlighting

});
```

## what is changed in the code?

The only thing changed is the curly brackets in rehype-pretty-code regex because because MDsveX converts to HTML symbols.

Specifically:
```javascript
 // rehype-pretty-code index.js

// const strippedValue = value.replace(/{:[a-zA-Z.-]+}/, ''); // old
const strippedValue = value.replace(/&#123;:[a-zA-Z.-]+&#125;/, '');
console.log("strippedValue", strippedValue);
// const meta = value.match(/{:([a-zA-Z.-]+)}$/)?.[1]; // old
const meta = value.match(/&#123;:([a-zA-Z.-]+)&#125;$/)?.[1];
```

## still broken

the token feature `{:.token}` is still broken. when i figure this out i'll make a PR
 
