<template>
    <div class="container">
        <div id="app">
            <h1>{{ title }}</h1>

            <p>{{ message }} : {{ selectedType }}</p>

            <div>
                <input name="inputValue" v-model.trim="message" placeholder='write goal or task...' />
                <select  v-model="selectedType">
                    <option disabled value="">Choose type</option>
                    <option value="important_urgent">important+urgent</option>
                    <option value="important_nonurgent">important+non-urgent</option>
                    <option value="unimportant_urgent">important+non-urgent</option>
                    <option value="unimportant_nonurgent">unimportant+non-urgent</option>
                </select>
                <input type='submit' value='add'  v-on:click="handleSubmit" />
            </div>

            <table>
                <tbody>
                <tr>
                    <td>
                        <b>Important+Urgent</b>
                        <ul>
                            <li v-for="value in items.important_urgent" :key="index">
                                {{ value }}
                            </li>
                        </ul>
                    </td>
                    <td>
                        <b>Unimportant+Urgent</b>
                        <ul>
                            <li v-for="value in items.unimportant_urgent" :key="index">
                                {{ value }}
                            </li>
                        </ul>
                    </td>
                </tr>
                <tr>
                    <td>
                        <b>Important+Non-urgent</b>
                        <ul>
                            <li v-for="value in items.important_nonurgent" :key="index">
                                {{ value }}
                            </li>
                        </ul>
                    </td>
                    <td>
                        <b>Unimportant+Non-urgent</b>
                        <ul>
                            <li v-for="value in items.unimportant_nonurgent" :key="index">
                                {{ value }}
                            </li>
                        </ul>
                    </td>
                </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'app',
        created() {
            console.log('App component was created');
        },
        data() {
            return {
                title: 'Priorities',
                message: '',
                selectedType: '',
                items: {
                    'important_urgent': [],
                    'important_nonurgent': [],
                    'unimportant_urgent': [],
                    'unimportant_nonurgent': []
                }
            }
        },
        methods: {
            handleSubmit: function() {
                const value = this.message,
                    type = this.selectedType;

                if(!value || !type) return false;
                this.message = '';
                this.selectedType = '';

                this.items[type].push(value);
            }
        }
    }
</script>

<style lang="css">
    #app {
        color: #56b983;
    }

    b {
        color: #000;
    }
    
    td {
        padding: 5px 10px;
        border: 1px seagreen solid;
        vertical-align: top;
    }
</style>