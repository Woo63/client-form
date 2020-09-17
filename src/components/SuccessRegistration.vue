<template>
    <transition name="modal-fade">
        <div class="successWindow">
            <div class="modal" role="dialog">
                <h2>{{name}}, Вы  успешно зарегистрированы!</h2>
                <button type="submit" @click="onClose" class="close">x</button>
            </div>
        </div>
    </transition>
</template>

<script>
    export default {
        props:['name', 'view','onClose'],
        name: "SuccessRegistration"
    }
</script>

<style scoped>
    .successWindow{
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        background-color: rgba(0, 0, 0, 0.3);
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .modal {
        background-color: #b3d7ff;
        box-shadow: 2px 2px 20px 1px;
        overflow-x: auto;
        display: flex;
        justify-content: space-between;
        border: 2px solid rgba(63, 128, 174, 0.93);
        border-radius: 10px;
    }
    .close {
        border: none;
        font-size: 20px;
        padding: 20px;
        cursor: pointer;
        font-weight: bold;
        color: #0b76ef;
        background: transparent;
        outline: none;
    }
    h2{
        display: block;
        font-size: 20px;
        padding: 5% 0 5% 10%;
    }
    .modal-fade-enter,
    .modal-fade-leave-active {
        opacity: 0;
    }
    .modal-fade-enter-active,
    .modal-fade-leave-active {
        transition: opacity 0.5s ease;
    }
</style>