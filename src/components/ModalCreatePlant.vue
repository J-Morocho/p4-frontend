<template>
    <section>
        <button class="button is-info is-small"
            @click="isComponentModalActive = true">
            Add Plant
        </button>

        <b-modal 
            v-model="isComponentModalActive"
            has-modal-card
            trap-focus
            :destroy-on-hide="false"
            aria-role="dialog"
            aria-modal>
            
            <ModalFormPlant v-bind="formProps"/>
        </b-modal>
    </section>
</template>

<script>
import ModalFormPlant from './ModalFormPlant'

export default {
    name: 'ModalCreatePlant',
    props: ['user', 'credentials'],
    components: {
        ModalFormPlant
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