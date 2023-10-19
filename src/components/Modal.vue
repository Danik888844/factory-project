<template>
  <div class="backdrop" @click.self="closeModal">
    <div class="modal">
        <h2>Добавление фабрики в cookie</h2>
        <form>
            <label>Город: </label>
            <select required>
                <option v-for="city in cities" :key="city.ID" :value="city.ID">{{ city.CityName }}</option>
            </select>
            <label>Цех: </label>
            <select required>
                <option v-for="city in cities" :key="city.ID" :value="city.ID">{{ city.CityName }}</option>
            </select>
            <label>Работник: </label>
            <select required>
                <option v-for="city in cities" :key="city.ID" :value="city.ID">{{ city.CityName }}</option>
            </select>
            <label>Бригада: </label>
            <select required>
                <option v-for="city in cities" :key="city.ID" :value="city.ID">{{ city.CityName }}</option>
            </select>
            <label>Смена: </label>
            <select required>
                <option v-for="city in cities" :key="city.ID" :value="city.ID">{{ city.CityName }}</option>
            </select>

            <input type="submit" style="margin-top: 25px;" />
        </form>
    </div>
  </div>
</template>

<script>
export default {
    props: ['cities'],
    methods: {
        closeModal(){
            this.$emit('close')
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