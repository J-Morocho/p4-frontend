<template>
    <section>
        <button class="button is-primary is-medium"
            @click="isComponentModalActive = true">
            Launch component modal
        </button>

        <b-modal 
            v-model="isComponentModalActive"
            has-modal-card
            trap-focus
            :destroy-on-hide="false"
            aria-role="dialog"
            aria-modal>
            
            <ModalFormCategory v-bind="formProps"/>
        </b-modal>
    </section>
</template>

<script>
import ModalFormCategory from './ModalFormCategory'

export default {
    name: 'ModalCreateCategory',
    components: {
        ModalFormCategory
    },
    data: function() {
        return {
            isComponentModalActive: false,
            formProps: {
                email: 'evan@you.com',
                password: 'testing'
            }
        }
    }
}
</script>