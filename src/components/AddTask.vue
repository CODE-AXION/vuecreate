<template>
    <div>
        <form @submit="addTaskForm" action="">
            <div>
                <label for="">Enter Your Event Name: </label>
                <input type="text" v-model="event" name="event" id="">
                <select name="status" v-model="status" id="">

                    <option value="true">Enable</option>
                    <option value="false">disable</option>
                </select>
               <input type="submit" value="Save Task" class="btn btn-block" />
            </div>
        </form>
    </div>
</template>

<script>

export default {
    name: 'AddTaskComponent',

    data(){

        return {
            event: '',
            status: 'true'
        }
    },

     methods: {
        addTaskForm(e) {

        e.preventDefault()
        if (!this.event) {
            alert('Please add a event')
            return
        }
        const newTask = {
            text: this.event,
            status: this.status,
        }

        this.$emit('add-event', newTask)

        console.log(newTask)

        this.event = ''
        this.status = false
        },
  },
}
</script>