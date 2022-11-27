<template>
    <section class="interactive-card">
        <div class="cards-side">
            <div class="cards">
                <CardBack :cvc="formData.cvc"/>
                <CardFront :cardholder-name="formData.cardholderName" :card-number="formData.cardNumber" :month="formData.month" :year="formData.year"/>
            </div>
        </div>
        <div class="form-side">
            <div class="form-container">
                <form class="form">
                <div class="form-group">
                    <label for="cardholder-name" class="form-group__label">Cardholder name</label>
                    <input type="text" id="cardholder-name" class="form-group__input" :class="{ 'form-group__input--error': $v.cardholderName.$error}" v-model="formData.cardholderName" placeholder="e.g. Jane Appleseed">
                    <p v-if="$v.cardholderName.$error" class="error-message">
                        {{$v.cardholderName.$errors[0].$message}}
                    </p>
                </div>
                
                <div class="form-group">
                    <label for="card-number" class="form-group__label">Card number</label>
                    <input type="text" maxlength="16" id="card-number" class="form-group__input" :class="{ 'form-group__input--error': $v.cardNumber.$error}" v-model="formData.cardNumber" placeholder="e.g. 1234 5678 9123 0000">
                    <p v-if="$v.cardNumber.$error" class="error-message">
                        {{$v.cardNumber.$errors[0].$message}}
                    </p>
                </div>

                <div class="form-group form-group--short">
                    <label class="form-group__label">Exp.&nbsp;date&nbsp;(mm/yy)</label>
                    <div class="card-date">
                        <div class="card-date__month">
                            <input type="text" maxlength="2" class="form-group__input form-group__input--date" :class="{ 'form-group__input--error': $v.month.$error}" v-model="formData.month" placeholder="MM">
                            <p class="error-message" v-if="$v.month.$error">{{$v.month.$errors[0].$message}}></p>
                        </div>
                        <div class="card-date__year">
                            <input type="text" maxlength="4" class="form-group__input form-group__input--date" :class="{ 'form-group__input--error': $v.year.$error}" v-model="formData.year" placeholder="YY">
                            <p class="error-message" v-if="$v.year.$error">{{$v.year.$errors[0].$message}}></p>
                        </div>
                    </div>

                </div>
                
                <div class="form-group form-group--short">
                    <label for="cvc" class="form-group__label">CVC</label>
                    <input type="text" maxlength="3" id="cvc" class="form-group__input" :class="{ 'form-group__input--error': $v.cvc.$error}" v-model="formData.cvc" placeholder="e.g. 123">
                    <p v-if="$v.cvc.$error" class="error-message">
                        {{$v.cvc.$errors[0].$message}}
                    </p>
                </div> 
                <ConfirmButton @submit="submitForm" btn-text="Confirm"/>
            </form>
            </div>
            <FormAlert v-if="isFormValid" :closeFormAlert="closeFormAlert"/>
        </div>
    </section>

</template>

<script setup>
    import { ref, reactive, computed } from 'vue';
    import { useVuelidate } from '@vuelidate/core'
    import { required, integer, minLength, between, helpers } from '@vuelidate/validators'
    import CardFront from './CardFront.vue';
    import CardBack from './CardBack.vue';
    import ConfirmButton from './ConfirmButton.vue';
    import FormAlert from './FormAlert.vue';

    const currentYear = new Date().getFullYear()
    const isFormValid = ref(false);

    const cardNumberLength = (value)=>{
        return value.length === 16;
    }

    const lettersOnly = (value)=>{
        const pattern = /^[A-Za-z\s]*$/
        return pattern.test(value)
    }

    const formData = reactive({
        cardholderName: '',
        cardNumber: '',
        month: '',
        year: '',
        cvc: ''
    })

    const rules = computed(()=>{
        return {
            cardholderName: {
                required: helpers.withMessage('Cardholder name is required', required),
                minLength: minLength(4),
                lettersOnly: helpers.withMessage('The name should contain only letters', lettersOnly)
            },
            cardNumber: { 
                required: helpers.withMessage('Card number is required', required),
                integer,
                cardNumberLength: helpers.withMessage('The card must have 16 digits', cardNumberLength) 
            },
            month: { 
                required: helpers.withMessage('Month is required',required),
                integer,
                between: between(1,12),
            },
            year: {
            required: helpers.withMessage('Year is required', required),
            integer,
            between: between(currentYear, currentYear+20)
            },
            cvc: {
                required: helpers.withMessage('CVC is required', required),
                integer,
                minLength: minLength(3)
            }
        }
    })

    const $v = useVuelidate(rules, formData)

    const submitForm = async ()=>{
        const result = await $v.value.$validate()
        if(result){
            isFormValid.value = true;
        }
    }
    const closeFormAlert = () =>{
        isFormValid.value = false;
    }
</script>   

<style lang="scss" scoped>
    .interactive-card{
        display: flex;
        flex-direction: column;
    }
    .cards-side{
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        background-image: url('../assets/images/bg-main-mobile.png');
        background-size: cover;
        min-height: 30vh;
        margin-bottom: 3em;
        .cards{
        position: absolute;
        top: 2em;
        width: 100%;
        display: flex;
        align-items: center;
        flex-direction: column;
        }
    }
    .form-side{
            position:relative;
            display: flex;
    }
    .form-container{
        width: 90%;
        margin: 0 auto;
        .form{
            display: flex;
            flex-wrap: wrap;
            .form-group{
                width: 100%;
                display: flex;
                flex-direction: column;
                text-transform: uppercase;
                margin-bottom: 1em;
                &__label{
                    font-size: 12px;
                    font-weight: bold;
                    color: var(--very-dark-violet);
                    letter-spacing: 2px;
                    padding: 5px;
                }
                .error-message{
                    font-size: 10px;
                    text-transform: initial;
                    margin-top: 5px;
                    color: var(--error-input);
                }
                &--short{
                    width: 50%;
                }
                &__input{
                    font-size: 14px;
                    padding: 10px;
                    border: 1px solid var(--light-grayish-violet);
                    border-radius: 10px;
                    &:focus{
                        outline: 1px solid var(--active-input);  
                    }
                    &--date{
                        width: 100%;
                    }
                    &--error{
                        border: 1px solid var(--error-input);
                    }
                }
                .card-date{
                    display: flex;
                    &__year{
                        margin: 0 20px 0 5px;
                    }
                }
            }
        }
    }
    @media(min-width: 375px){
        .cards-side{
            margin-bottom: 5em;
        }
    }
    @media(min-width: 768px){
        .cards-side{
            margin-bottom: 9em;
        }
    }
    @media(min-width: 992px){
        .interactive-card{
            flex-direction: row;
        }
        .cards-side{
            width: 35%;
            height: 100vh;
            background-image: url('../assets/images/bg-main-desktop.png');
            margin: 0;
            .cards{
                top: 50%;
                transform: translateY(-50%);
                flex-direction: column-reverse;
                left: 40%
            }
        }
        .form-side{
            height: 100vh;
            justify-content: center;
            align-items: center;
            .form-container{
                width: 40%;
                min-width: 300px;
                margin-left: 35%;
                .form-group{
                    margin-bottom: 0.8em;
                    &__label{
                        font-size: 10px;
                    }
                    &__input{
                        font-size: 12px;
                    }
                }
            }
        }
    }
</style>