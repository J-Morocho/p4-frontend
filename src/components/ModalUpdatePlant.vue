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
            
            <ModalFormUpdatePlant v-bind='formProps'/>
        </b-modal>
    </section>
</template>

<script>
import ModalFormUpdatePlant from './ModalFormUpdatePlant'

export default {
    name: 'ModalUpdatePlant',
    props: ['user', 'credentials'],
    components: {
        ModalFormUpdatePlant,
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