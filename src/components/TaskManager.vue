<template>
    <div class="container task-manager">
        <div style="margin: 5px 0 20px 0;">
            <center><h2 style="margin: 20px auto;">Tasks Manager</h2></center>
            <h5 v-if="filterNotCompleted(tasks).length" style="margin-bottom: 10px;">
				New Tasks ({{ filterNotCompleted(tasks).length }})
			</h5>
            <ol class="list-group">
                <li v-for="task in filterNotCompleted(tasks)" 
					:key="task.name" 
					v-on:dblclick="editTask(task)"
					title="Double click to edit!" 
					class="list-group-item">{{task.name}}

						<button v-on:click="removeTask(task)">
							<i class="fa fa-trash"></i>
						</button>
						<button v-on:click="completeTask(task)">
							<i style="color: #10B336;" class="fa fa-check-square"></i>
						</button>
                </li>
            </ol>
        </div>

        <form>
            <div class="form-group">
                <input style="margin-bottom: 10px;" 
                    ref='newtask'
                    v-model="newTask" 
                    class="form-control" 
                    placeholder="Enter your new task ...">

                <button v-on:click="addTask" class="btn btn-info" type="submit">Add</button>
                <button v-on:click="completeAllTasks" class="btn btn-success">Complete All</button>
            </div>
        </form>
        <div v-if="filterCompleted(tasks).length" style="margin: 20px 0 10px 0; border-top: 1px solid#DBDBDB;">
            <h5 style="margin: 10px 0;">Completed Tasks ({{ filterCompleted(tasks).length }})</h5>
            <ol class="list-group">
                <li v-for="task in filterCompleted(tasks)" :key="task.name" class="list-group-item">
                    {{task.name}}
                    <button v-on:click="removeTask(task)">
                        <i class="fa fa-trash"></i>
                    </button>
                </li>
            </ol>

        </div>
        <br>
        <pre>{{$data | json}}</pre>
    </div>
</template>

<script>
export default {
    name: 'task-manager',
	data: function(){
		return{
			tasks: [
				{name: 'Đi chợ', completed: false},
				{name: 'Nấu cơm', completed: false},
				{name: 'Tập yoga', completed: false},
			],

			newTask: ''
		}
	},

	methods: {
		addTask: function(e){
			e.preventDefault();
			this.tasks.push({
				name: this.newTask,
				completed: false
			});

			this.newTask = '';
		},

		removeTask: function(task){
			this.tasks.splice(this.tasks.indexOf(task), 1);
		},

		editTask: function(task){
			//remove task
			this.removeTask(task);
			
			//update input
			this.newTask = task.name;

			//input focus
			this.$refs.newtask.focus();
		},

		completeTask: task => {
			task.completed = true;
		},

		completeAllTasks: function (e){
			e.preventDefault();
			console.log('completed all');
			this.tasks.forEach(task => {
				task.completed = true;
			});
		},

		//****************
		filterNotCompleted: tasks => {
			return tasks.filter( task => !task.completed);
		},

		filterCompleted: tasks =>{
			return tasks.filter( task => task.completed);
		}
	}
}
</script>

<style scoped>
	ol li button{
		cursor: pointer;
		font-weight: bold;
		color: red;
		background: none;
		border: 0;
		padding: 0;
		margin-left: 10px;
		float: right;
	}

	ol li:hover{
		cursor: pointer;
		background-color: #EDEDED;
	}
	.btn-info{
		margin-right: .5rem;
	}
</style>

