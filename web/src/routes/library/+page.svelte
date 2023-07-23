<script lang="ts">
	import { Search, Card, Table, TableBody, TableBodyCell, TableBodyRow } from 'flowbite-svelte';

	let ISBN = '';
	ISBN = '0451526538';

	let book = {
        cover: '',
		title: '',
		author: '',
		byStatement: '',
		pages: '',
		publisher: '',
		publishedDate: '',
		categories: ''
	};

	async function searchBook(ISBN: string) {
		const url = `https://openlibrary.org/api/books?jscmd=data&format=json&bibkeys=ISBN:${ISBN}`;
		const res = await fetch(url);
		const data = await res.json();
		const bookData = data[`ISBN:${ISBN}`];
        if (!bookData) {
            alert('Book not found!');
            return;
        }
		book = {
            cover: bookData.cover.medium,
			title: bookData.title,
			author: bookData.authors[0].name,
			byStatement: bookData.by_statement,
			pages: bookData.number_of_pages.toString(),
			publisher: bookData.publishers[0].name,
			publishedDate: bookData.publish_date,
			categories: parseSubjectsListToStr(bookData.subjects),
		};
		console.log(book);
	}

    function parseSubjectsListToStr(subjects: {name: string}[]) {
        let str = '';
        for (let subject of subjects) {
            str += subject.name + ', ';
        }
        return str.slice(0, -2);
    }
</script>

<h1 class="text-6xl text-white">Recursion Library</h1>
<form on:submit|preventDefault={() => searchBook(ISBN)} class="flex gap-2 mt-4">
	<Search size="lg" bind:value={ISBN} />
</form>

<Card class="mt-5 w-full max-w-md mx-auto bg-white rounded-xl shadow-md overflow-hidden">
	<div class="p-8">
		<h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900">{book.title}</h5>
		<p class="mb-3 text-gray-700">{book.author}</p>
		<p class="font-normal text-gray-700 leading-tight">
			{book.byStatement}
		</p>
	</div>
    <img src={book.cover} class="card-img p-3" alt="">
	<Table>
		<TableBody>
			<TableBodyRow>
				<TableBodyCell>Page</TableBodyCell>
				<TableBodyCell>{book.pages}</TableBodyCell>
			</TableBodyRow>
			<TableBodyRow>
				<TableBodyCell>Publisher</TableBodyCell>
				<TableBodyCell>{book.publisher}</TableBodyCell>
			</TableBodyRow>
			<TableBodyRow>
				<TableBodyCell>Published Date</TableBodyCell>
				<TableBodyCell>{book.publishedDate}</TableBodyCell>
			</TableBodyRow>
			<TableBodyRow>
				<TableBodyCell>Categories</TableBodyCell>
				<TableBodyCell>{book.categories}</TableBodyCell>
			</TableBodyRow>
		</TableBody>
	</Table>
</Card>


