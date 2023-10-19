<template>
  <div class="backdrop" @click.self="closeModal">
    <div class="modal">
        <h2>Добавление фабрики в cookie</h2>
        <form>
            <label>Город: </label>
            <select @change="getGilds" v-model="city">
                <option v-for="city in cities" :key="city.id" :value="city">{{ city.CityName }}</option>
            </select>
            <label>Цех: </label>
            <select @change="getEmployees" v-model="gild">
                <option v-for="gild in gilds" :key="gild.id" :value="gild">{{ gild.GildName }}</option>
            </select>
            <label>Работник: </label>
            <select v-model="employee">
                <option v-for="employee in employees" :key="employee.id" :value="employee">{{ employee.FullName }}</option>
            </select>
            <label>Бригада: </label>
            <select v-model="brigade">
                <option v-for="brigade in brigades" :key="brigade.id" :value="brigade">{{ brigade.BrigadeName }}</option>
            </select>
            <label>Смена: </label>
            <select v-model="shift">
                <option v-for="shift in shifts" :key="shift.id" :value="shift">{{ shift.ShiftName }}</option>
            </select>

            <button style="margin-top: 25px;width: 100%;" @click="saveData">Сохранить в Cookie</button>
        </form>
    </div>
  </div>
</template>

<script>
import VueCookies from "vue-cookie";

export default {
    data(){
        return{
            city: null,
            gild: null,
            employee: null,
            brigade: null,
            shift: null,
            gilds: [],
            employees: []
        }
    },
    props: ['cities','brigades','shifts','factories'],
    methods: {
        closeModal(){
            this.$emit('close')
        },
        saveData() {
            const newFactory = {
                CityName: this.city.CityName,
                GildName: this.gild.GildName,
                FullName: this.employee.FullName,
                BrigadeName: this.brigade.BrigadeName,
                ShiftName: this.shift.ShiftName
            };

            this.factories.push(newFactory);
            VueCookies.set("savedData", JSON.stringify(this.factories), 1);

            this.gilds = []
            this.employees = []
        },
        getGilds(){
            if(!this.city)
                return null;

            this.gilds = []
            this.employees = []
            for (const gildId of this.city.Gilds){
                fetch('http://localhost:3000/gilds/'+gildId)
                .then((res)=>res.json())
                .then(data => this.gilds.push(data))
                .catch(err => console.log(err.message))
            }
        },
        getEmployees(){
            if(!this.gild)
                return null;

            this.employees = []
            for (const employeeId of this.gild.Employees){
                fetch('http://localhost:3000/employees/'+employeeId)
                .then((res)=>res.json())
                .then(data => this.employees.push(data))
                .catch(err => console.log(err.message))
            }
        }
    }
}
</script>

<style>
    .modal {
        max-width: 600px;
        max-height: 500px;
        padding: 20px;
        margin: 100px auto;
        background: white;
        border-radius: 5px;
        overflow: auto;
    }
    .backdrop {
        top: 0;
        position: fixed;
        background: rgba(0,0,0,0.5);
        width: 100%;
        height: 100%;
    }
</style>