<script>
	import { authHandlers, authStore } from '../../store/store';
	import { getDoc, doc, setDoc } from 'firebase/firestore';
	import { db } from '../../lib/firebase/firebase';

	let todoList = ['Follow Shubham Bane on LinkedIn'];
	let newTodo = '';
	let error = false;

	authStore.subscribe((curr) => {
		todoList = curr.data.todos;
	});

	function addTodo() {
		error = false;
		if (!newTodo) {
			error = true;
			alert('Empty Task!');
			return;
		}
		todoList = [...todoList, newTodo];
		newTodo = '';
	}

	function editTodo(index) {
		let newTodoList = [...todoList].filter((val, i) => {
			return i != index;
		});

		newTodo = todoList[index];
		todoList = newTodoList;
	}

	function deleteTodo(index) {
		let newTodoList = [...todoList].filter((val, i) => {
			return i != index;
		});

		todoList = newTodoList;
	}
	async function saveTodos() {
		try {
			const userRef = doc(db, 'users', $authStore.user.uid);
			await setDoc(
				userRef,
				{
					todos: todoList
				},
				{ merge: true }
			);
		} catch (err) {
			console.log('There was an error saving your information');
		}
	}
</script>

{#if $authStore.loading}
	<p>Loading...</p>
{/if}
{#if !$authStore.loading}
	<div class="mainContainer">
		<div class="headerContainer">
			<h1>Todo List</h1>
			<div class="headerBtn">
				<button on:click={saveTodos}
					><i class="fa-regular fa-floppy-disk"></i>
					<p>Save</p></button
				>
				<button on:click={authHandlers.logout}>
					<i class="fa-solid fa-arrow-right-from-bracket"></i>
					<p>Logout</p></button
				>
			</div>
		</div>
		<main>
			{#if todoList.length === 0}
				<p>You have nothing to do!</p>
			{/if}
			{#each todoList as todo, index}
				<div class="todo">
					<p>
						{index + 1}. {todo}
					</p>
					<div class="actions">
						<i
							on:click={() => {
								editTodo(index);
							}}
							on:keydown={() => {}}
							aria-hidden="true"
							class="fa-regular fa-pen-to-square"
						></i>
						<i
							on:click={() => {
								deleteTodo(index);
							}}
							on:keydown={() => {}}
							aria-hidden="true"
							class="fa-regular fa-trash-can"
						></i>
					</div>
				</div>
			{/each}
		</main>
		<div class={'enterTodo ' + (error ? 'errorBorder' : '')}>
			<input bind:value={newTodo} type="text" placeholder="Enter a todo" />
			<button on:click={addTodo}>Add</button>
		</div>
	</div>
{/if}

<style>
	.mainContainer {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
		gap: 24px;
		padding: 24px;
		width: 100%;
		max-width: 1000px;
		margin: 0 auto;
	}

	.headerContainer {
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.headerContainer button {
		background: #000;
		color: #fff;
		padding: 12px 24px;
		border: none;
		font-weight: 700;
		border-radius: 8px;
		display: flex;
		align-self: center;
		gap: 8px;
	}

	.headerContainer button i {
		font-size: 1.1em;
	}

	.headerContainer button:hover {
		background: #383838;
	}

	.headerBtn {
		display: flex;
		align-items: center;
		gap: 16px;
	}

	main {
		display: flex;
		flex-direction: column;
		gap: 16px;
		flex: 1;
	}

	.todo {
		border-left: 1px solid #aaaaaa;
		padding: 16px;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.actions {
		display: flex;
		gap: 16px;
		font-size: 1.2em;
		align-items: center;
	}

	.actions i {
		cursor: pointer;
	}

	.actions i:hover {
		color: #0f2167;
	}

	.enterTodo {
		display: flex;
		align-items: stretch;
		border: 1px solid #aaaaaa;
		border-radius: 8px;
		overflow: hidden;
	}

	.errorBorder {
		border: 1px solid #ff0000 !important;
	}

	.enterTodo input {
		flex: 1;
		background: transparent;
		border: none;
		padding: 16px;
	}

	.enterTodo input:focus {
		outline: none;
	}

	.enterTodo button:hover {
		background: #222222;
	}

	.enterTodo button {
		background: #000;
		color: #fff;
		border: none;
		padding: 8px 24px;
		border-radius: 8px;
		cursor: pointer;
	}
</style>
