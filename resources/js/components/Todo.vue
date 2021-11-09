<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card mt-5">
                    <Label class="card-header" value="Add a ToDo"></Label>
                    <div class="card-body d-flex">
                        <add-input v-model="newTask" v-on:keyup.enter.native="addTask" type="text" :value="newTask" ></add-input>
                        <Button v-on:click.native="addTask" class="btn btn-outline-secondary" type="submit" value="ADD"></Button>

                    </div>
                </div>
            </div>
        </div>

        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card mt-5">
                    <Label class="card-header" value="List of added tasks"></Label>
                    <ul class="card-body p-4">
                        <li v-for="(task, n) in tasks" class="d-flex align-items-center justify-content-between py-1">
                            <span :class="{'cc': task.completed}">{{task.todo}}</span>
                            <div class="d-flex">
                                <Button v-on:click.native="removeTask(n)" class="btn btn-outline-secondary mr-2" type="submit" value="Delete task"></Button>
                                <Button v-on:click.native="toggleCompletedTask(n)" class="btn btn-outline-secondary" value="Completed"></Button>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>

</template>

<script>

    export default {

        data() {
            return {
                newTask: "",
                tasks: [
                    {
                      todo: 'String',
                      completed: false
                    }
                ],
            }
        },

        mounted() {
            if(localStorage.getItem('listOfTasks')) {
                try {
                    this.tasks = JSON.parse(localStorage.getItem('listOfTasks'));
                }
                catch(e) {
                    localStorage.removeItem('listOfTasks');
                }
            }
        },

        methods: {
            addTask() {
                if(this.newTask.length !=0) {
                    this.tasks.push({
                        todo: this.newTask,
                        completed: false
                    });
                    this.newTask= '';
                    this.saveTask();
                }
            },

            saveTask() {
                let parsed = JSON.stringify(this.tasks);
                localStorage.setItem('listOfTasks', parsed);
            },

            removeTask(i) {
                this.tasks.splice(i,1);
                this.saveTask();
            },

            toggleCompletedTask(index) {
                const taskCopy = [...this.tasks]
                taskCopy[index].completed = !taskCopy[index].completed;
                this.tasks = taskCopy
                this.saveTask()
            }
        },
    }
</script>
