<template>
    <section>
        <button class="button is-info is-small"
            @click="isComponentModalActive = true">
            New Category
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
    props: ['user', 'credentials'],
    components: {
        ModalFormCategory
    },
    data: function() {
        return {
            isComponentModalActive: false,
            formProps: {
                user: this.user,
                credentials: this.credentials
            }
        }
    }
}
</script>