<script>
	import Book from './book.svelte'
	import Button from './button.svelte'
	import Purchase from './purchase.svelte'

	let title = '';
	let price = 0;
	let description = '';

	let books =[];
	let purchases = [];

	function setTitle(event){
		title = event.target.value;
	}

	function addBook(){
		const newBook = {
			title : title,
			price : price,
			description: description

		};
		books = books.concat(newBook)
	}

	function purchaseBook(event){
		const selectedTitle= event.detail;
		purchases = purchases.concat({
			...books.find(book => book.title === selectedTitle)
		});
	}

</script>

<style>
	h1 {
		color: purple;
		text-align:center;

	}

	section{
		margin: 1rem auto;
		width: 30rem;
	}

	label,input,textarea{width: 100%}
</style>

<h1>Book Store</h1>

<section>
	<h2>Add New Book</h2>
	<div>
		<label for="title">Title</label>
		<input type="text" id="title" value={title} on:input={setTitle}/>
	</div>

	<div>
		<label for="price"> Price</label>
		<input type="number" id="price" value={price} name="bind:value={price}"/>
	</div>

	<div>
		<label for="description">Description</label>
		<textarea rows="3" id="description" bind:value={description}/>
	</div>

	<Button on:click={addBook}>ADD Book</Button>

</section>

<section>
	<h2>Stock</h2>
	{#if books.length === 0}
		<p>
			No books in stock.
		</p>
	{:else}
	{#each books as book}
		<Book bookTitle={book.title}
		bookPrice={book.price}
		bookDescription={book.description}
		on:buy={purchaseBook}
		/>
	{/each}
{/if}
</section>

<section>
	<Purchase books ={purchases}  />
</section>
