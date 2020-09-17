<template>
    <form @submit.prevent="onRegistration">
        <div class="block">
            <h2>Контактная информация</h2>
            <small>* Поле обязательное для заполнения.</small>
            <label>Фамилия *
                <input
                        type="text"
                        v-model.trim="userData.surname"
                        :class="{invalid: ($v.userData.surname.$dirty && !$v.userData.surname.required)}"
                >
                <small
                        class="invalid"
                        v-if="$v.userData.surname.$dirty && !$v.userData.surname.required"
                >
                    Поле не должно быть пустым!
                </small>
            </label>
            <label>Имя *
                <input
                        type="text"
                        v-model.trim="userData.name"
                        :class="{invalid: ($v.userData.name.$dirty && !$v.userData.name.required) }"
                >
                <small
                        class="invalid"
                        v-if="$v.userData.name.$dirty && !$v.userData.name.required"
                >
                    Поле не должно быть пустым!
                </small>
            </label>
            <label>Отчество
                <input type="text" v-model="userData.lastname">
            </label>
            <label>Номер телефона *
                <input
                        type="text"
                        v-model="userData.phone"
                        placeholder="7(XXX)-XXX-XX-XX"
                        maxlength="11"
                        onkeyup="this.value = this.value.replace(/[^\d]/g,'')"
                        :class="{invalid: ($v.userData.phone.$dirty && (!$v.userData.phone.required || !$v.userData.phone.phoneValid || !$v.userData.phone.minLength))}"
                >
                <small
                        class="invalid"
                        v-if="$v.userData.phone.$dirty && !$v.userData.phone.required"
                >
                    Поле не должно быть пустым!
                </small>
                <small
                        class="invalid"
                        v-if="$v.userData.phone.$dirty && (!$v.userData.phone.phoneValid || !$v.userData.phone.minLength)"
                >
                    Введите корректный телефонный номер!
                </small>
            </label>
            <div class="radio">
                <span>Пол</span>
                <input type="radio" id="male" value="мужской" v-model="userData.sex" class="radio-control male">
                <label for="male">мужской</label>
                <input type="radio" id="female" value="женский" v-model="userData.sex" class="radio-control female">
                <label for="female">женский</label>
            </div>
            <span>Группа клиентов *</span>
            <div class="group">
                <input id="vip" type="checkbox" v-model="userData.clientGroup" class="custom-checkbox" value="VIP">
                <label for="vip">VIP</label>
                <input id="problem" type="checkbox" v-model="userData.clientGroup" class="custom-checkbox"
                       value="Проблемные">
                <label for="problem">Проблемные</label>
                <input id="oms" type="checkbox" v-model="userData.clientGroup" class="custom-checkbox" value="ОМС">
                <label for="oms">ОМС</label>
            </div>
            <small
                    class="invalid"
                    v-if="$v.userData.clientGroup.$dirty && !$v.userData.clientGroup.required"
            >
                Поле не должно быть пустым!
            </small>
            <label class="select">Лечащий врач
                <select v-model="userData.doctor">
                    <option v-for="option in optionsDoctor"
                            v-bind:value="option.value"
                            v-bind:key="option.value"
                    >
                        {{ option.text }}
                    </option>
                </select>
            </label>
            <input id="sms" type="checkbox" v-model="userData.sms" class="custom-checkbox">
            <label for="sms">Не отправлять СМС</label>
        </div>
        <div class="block">
            <h2>Адрес</h2>
            <label>Индекс
                <input
                        type="text"
                        v-model="userData.index"
                        onkeyup="this.value = this.value.replace(/[^\d]/g,'')"
                >
            </label>
            <label>Страна
                <input type="text" v-model="userData.country">
            </label>
            <label>Область
                <input type="text" v-model="userData.region">
            </label>
            <label>Город *
                <input
                        type="text"
                        v-model="userData.city"
                        :class="{invalid:($v.userData.city.$dirty && !$v.userData.city.required)}"
                >
                <small
                        class="invalid"
                        v-if="$v.userData.city.$dirty && !$v.userData.city.required"
                >
                    Поле не должно быть пустым!
                </small>
            </label>
            <label>Улица
                <input type="text" v-model="userData.street">
            </label>
            <label>Дом
                <input type="text" v-model="userData.house">
            </label>
        </div>
        <div class="block">
            <h2>Паспортные данные</h2>
            <label>Тип документа *
                <select
                        v-model="userData.optionDocument"
                        :class="{invalid: ($v.userData.optionDocument.$dirty && !$v.userData.optionDocument.required)}"
                >
                    <option v-for="option in documentOptions" v-bind:value="option.value" v-bind:key="option.value">
                        {{ option.text }}
                    </option>
                </select>
                <small
                        class="invalid"
                        v-if="$v.userData.optionDocument.$dirty && !$v.userData.optionDocument.required"
                >
                    Заполните поле!
                </small>
            </label>
            <label>Серия
                <input
                        type="text"
                        v-model="userData.seria"
                        maxlength="4"
                >
            </label>
            <label>Номер
                <input
                        type="text"
                        v-model="userData.number"
                        maxlength="6"
                        onkeyup="this.value = this.value.replace(/[^\d]/g,'')"
                >
            </label>
            <label>Кем выдан
                <input type="text" v-model="userData.place">
            </label>
            <label>Дата выдачи *
                <input
                        type="date"
                        v-model="userData.date"
                        :class="{invalid: ($v.userData.date.$dirty && !$v.userData.date.required)}"
                >
                <small
                        class="invalid"
                        v-if="$v.userData.date.$dirty && !$v.userData.date.required"
                >
                    Поле не должно быть пустым!
                </small>
                <small
                        class="invalid"
                        v-if="$v.userData.date.$dirty && !$v.userData.date.dateValid"
                >
                    Введите корректную дату!
                </small>
            </label>
        </div>
        <button type="submit">Зарегистрироваться</button>
    </form>

</template>

<script>
    import {required, numeric, minLength} from 'vuelidate/lib/validators'
    const phoneValid=(value)=>(
        (value.length)? (value[0]==='7') &&(numeric(value)):true
    )
    const dateValid=(value)=>{
        if (value.length){
            const now = new Date()
            const today = new Date(now.getFullYear(), now.getMonth(), now.getDate()).valueOf()
            const val=new Date(value)
            return (today>val.valueOf())
        }
        return true
    }
    const smoothJumpUp = function() {
        if (document.body.scrollTop>0 || document.documentElement.scrollTop>0) {
            window.scrollBy(0,-50);
            setTimeout(smoothJumpUp, 10);
        }
    }
    export default {
        name: "RegistrationForm",
        props:['onSubmit'],
        data(){
           return {
               userData:{
                   surname:'',
                   name:'',
                   lastname:'',
                   phone: '',
                   sex:'',
                   clientGroup:[],
                   doctor:'',
                   sms:false,
                   index:'',
                   country:'',
                   region:'',
                   city:'',
                   street:'',
                   house:'',
                   optionDocument:'',
                   seria:'',
                   number:'',
                   place:'',
                   date:''
               },
               optionsDoctor: [
                   {text:"Выберите врача", value:''},
                   {text:"Иванов", value:"Иванов"},
                   {text:"Захаров", value:"Захаров"},
                   {text:"Чернышева", value:"Чернышева"}
               ],
               documentOptions:[
                   {text:'Выберите тип документа', value:''},
                   {text:'Паспорт', value:'Паспорт'},
                   {text:'Свидетельство о рождении', value:'Свидетельство о рождении'},
                   {text:'Вод. удостоверение', value:'Вод. удостоверение'}
               ]
           }
        },
        validations:{
            userData: {
                surname:{required},
                name:{required},
                phone:{required, minLength: minLength(11), phoneValid},
                clientGroup: {required},
                city:{required},
                optionDocument: {required},
                date:{required, dateValid}
            }
        },
        methods:{
            onRegistration(){
                if (this.$v.$invalid) {
                    this.$v.$touch()
                    smoothJumpUp()
                    return
                }
                this.onSubmit(this.userData)
            }
        }
    }
</script>

<style lang="sass" scoped>
    $active-color: #0b76ef
    $shadow-color: rgba(0, 123, 255, 0.25)
    %text
        display: block
        font-size: 100%
        margin-bottom: 3%

    form
        position: relative
        justify-content: center
        display: flex
        flex-direction: column
        padding: 5%

    label,
    span
        @extend %text

    small
        @extend %text
        font-size: 80%
        opacity: 0.9
        &.invalid
            color: red
            margin-top: 1%

    input[type="text"], input[type="date"], select
        width: 100%
        padding: 10px 15px
        border-width: 0
        background: #e6e6e6
        outline: none
        margin: 2% 0 0
        box-sizing: border-box
        &:focus
            box-shadow: inset 0 0 0 2px rgba(0,0,0,.2)
    input[class="invalid"],
    input[class="invalid"]:active
        box-shadow: inset 0 0 0 2px rgba(242, 99, 99, 0.24)

    .radio-control
        position: absolute
        z-index: -1
        opacity: 0
        &+label
            display: flex
            align-items: center
            user-select: none
            &::before
                content: ''
                display: inline-block
                width: 2em
                height: 2em
                text-align: center
                border: 1px solid #adb5bd
                border-radius: 50%
                margin-right: 0.5em
                font-size: 100%
                background-repeat: no-repeat
                background-position: center center
                background-size: 70% 70%
        &.male+label::before
            background-image: url("../assets/male-solid.svg")
        &.female+label::before
            background-image: url("../assets/female-solid.svg")
        &:hover+label::before,
        &:focus+label::before
            box-shadow: 0 0 0 0.2rem $shadow-color
        &:checked+label::before
            border-color: $active-color
            background-color: $active-color

    select
        cursor: pointer
        outline: 0
        border: 0
        &:focus
            box-shadow: inset 0 0 0 2px rgba(0,0,0,.2)
        &::-ms-expand
            display: none
        &.invalid
            box-shadow: inset 0 0 0 2px rgba(242, 99, 99, 0.24)

    .group
        display: flex
        justify-content: space-between

    .custom-checkbox
        position: absolute
        z-index: -1
        opacity: 0
        &+label
            display: inline-flex
            align-items: center
            user-select: none
            &::before
                content: ''
                display: inline-block
                width: 1em
                height: 1em
                flex-shrink: 0
                flex-grow: 0
                border: 1px solid #adb5bd
                border-radius: 0.25em
                margin-right: 0.5em
                background-repeat: no-repeat
                background-position: center center
                background-size: 50% 50%
        &:checked+label::before
            border-color: $active-color
            background-color: $active-color
            background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8 8'%3e%3cpath fill='%23fff' d='M6.564.75l-3.59 3.612-1.538-1.55L0 4.26 2.974 7.25 8 2.193z'/%3e%3c/svg%3e")
        &:not(:disabled)
            &:not(:checked)+label:hover::before
                border-color: $shadow-color
            &:active+label::before
                background-color: $shadow-color
                border-color: $shadow-color
        &:focus
            &+label::before
                box-shadow: 0 0 0 0.2rem $shadow-color
            &:not(:checked)+label::before
                border-color: #80bdff
        &:disabled+label::before
            background-color: #e9ecef

    button
        margin-top: 10%
        border-radius: 5em
        border: 1px solid #adb5bd
        padding: 1em
        cursor: pointer
        outline: none
        &:hover,
        &:focus
            box-shadow: 0 0 0 0.2rem $shadow-color
        &:active
            background-color: $active-color

</style>