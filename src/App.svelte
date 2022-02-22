<script>
	import { v4 as uuidv4 } from 'uuid';
	import Button from './Button.svelte'

	let tasks = []

	let isEditing = false;



	let task = {
		id: '',
		desc:''
	}

	const addTask = () => {
		const newTask = {
			id: uuidv4(),
			desc: task.desc,
			done: false
		}

		if(newTask.desc.trim().length <= 0){
			return alert('La tarea no puede estar vacia')
		}
		
		tasks = tasks.concat(newTask)
	}

	const handleSubmit = () => {
		

		if(!isEditing){
			addTask()
			resetInput()
		}else{
			updateTask()
		}


	}

	const resetInput = () => {
		return task = {
			id: '',
			desc: ''
		}
	}

	const deleteTask = (id) => {

		tasks = tasks.filter( ( t ) => t.id !== id )

	}

	const editTask = (editedTask) => {
		
		task = editedTask;
		isEditing = true;

	}

	const updateTask = () => {
		let updatedTask = {
			id: task.id,
			desc: task.desc
		}

		const taskIndex = tasks.findIndex( (t) => t.id === task.id )
		tasks[taskIndex] = updatedTask;

		resetInput()
		isEditing = false;
	}


	const markAsDone = (task) => {

		let taskDone = {
			id: task.id,
			desc: task.desc,
			done: !task.done
		}


		let taskDoneIndex = tasks.findIndex( t => t.id === task.id )
		tasks[taskDoneIndex] = taskDone;

	
	}

	const clearDoneTasks = () => {

		tasks = tasks.filter( t => t.done !== true )


	}

	
		
</script>





<main>
	
	<h1>Task manager</h1>

	<form on:submit|preventDefault={handleSubmit}>

		<input type='text' bind:value={ task.desc } placeholder='Add task..'/>
	
		<Button type='submit' inverse={true}>
			{
				(!isEditing ? 'Add': 'Modify')
			}
		</Button>

	</form>

	<div class='results'>

		{#if tasks.length > 0}
			<h2>My tasks 
				<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-pencil-fill" viewBox="0 0 16 16">
				<path d="M12.854.146a.5.5 0 0 0-.707 0L10.5 1.793 14.207 5.5l1.647-1.646a.5.5 0 0 0 0-.708l-3-3zm.646 6.061L9.793 2.5 3.293 9H3.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.207l6.5-6.5zm-7.468 7.468A.5.5 0 0 1 6 13.5V13h-.5a.5.5 0 0 1-.5-.5V12h-.5a.5.5 0 0 1-.5-.5V11h-.5a.5.5 0 0 1-.5-.5V10h-.5a.499.499 0 0 1-.175-.032l-.179.178a.5.5 0 0 0-.11.168l-2 5a.5.5 0 0 0 .65.65l5-2a.5.5 0 0 0 .168-.11l.178-.178z"/>
			  </svg>
			</h2>
			{#if tasks.some((t) => t.done === true ) }
				<Button on:click={ clearDoneTasks } variant='danger' inverse={true}>Clear Done Tasks</Button>
			{/if}
			<ul>
				{#each tasks as task (task.id) }
				<li id={task.id} class:hecho={task.done}>
					<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-sticky" viewBox="0 0 16 16">
						<path d="M2.5 1A1.5 1.5 0 0 0 1 2.5v11A1.5 1.5 0 0 0 2.5 15h6.086a1.5 1.5 0 0 0 1.06-.44l4.915-4.914A1.5 1.5 0 0 0 15 8.586V2.5A1.5 1.5 0 0 0 13.5 1h-11zM2 2.5a.5.5 0 0 1 .5-.5h11a.5.5 0 0 1 .5.5V8H9.5A1.5 1.5 0 0 0 8 9.5V14H2.5a.5.5 0 0 1-.5-.5v-11zm7 11.293V9.5a.5.5 0 0 1 .5-.5h4.293L9 13.793z"/>
					</svg>
					{task.desc}
				</li>
				<Button variant='danger' inverse={true} on:click={ deleteTask(task.id) }>Delete</Button>
				<Button variant='secondary' inverse={true} on:click={ editTask(task)}>Edit</Button>
				<Button on:click={markAsDone(task)} inverse={true}>{task.done ? 'Undone': 'Done'}</Button>
				
				{/each}
			</ul>
		{:else}	
			<p>No tasks were added</p>
		
		{/if}
	</div> 

</main>

<style>


	main{
		margin: 0 auto;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	h1{
		font-family: 'Shizuru', cursive;
		color: white;
	}

	form{
		display:flex;
		flex-direction: column;
		justify-content: center;
	}

	h2{
		font-family: 'Roboto', sans-serif;
	}
	input{
		display: block;
		margin: 5px;
	
	}

	.results{
		margin: 10px;
		padding: 10px;
		border-radius: 4px;
		width: 50%;
		height: auto;
		display: flex;
		flex-direction: column;
		background-image: url('https://img.freepik.com/free-photo/white-crumpled-paper-background-simple-diy-craft_53876-128183.jpg?size=626&ext=jpg&ga=GA1.2.1521295508.1638748800');
	}

	

	.results p {
		text-align: center;
	}

	li{
		list-style-type: none;
		font-family: 'Roboto', sans-serif;
		border-bottom: 1px dashed #c7bfbf;
	}
	
	.hecho{
		text-decoration: line-through;
	}
	
</style>