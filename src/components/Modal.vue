<template>
  <div class="backdrop" @click.self="closeModal">
    <div class="modal">
        <h2>Добавить фабрику в cookie</h2>
        <div>
            <span>Город: </span>
            <input type="text" />
        </div>
    </div>
  </div>
</template>

<script>
export default {
    props: [],
    methods: {
        closeModal(){
            this.$emit('close')
        }
    }
}
</script>

<style>
    .modal {
        width: 600px;
        padding: 20px;
        margin: 100px auto;
        background: white;
        border-radius: 5px;
    }
    .backdrop {
        top: 0;
        position: fixed;
        background: rgba(0,0,0,0.5);
        width: 100%;
        height: 100%;
    }
</style>