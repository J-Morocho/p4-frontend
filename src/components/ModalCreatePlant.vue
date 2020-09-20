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
            <!-- We still need to refresh after plants are updated -->
            <ModalFormPlant :url='URL'
                            :user='credentials' 
                            :cat_id='category_id' 
                            @close='isComponentModalActive = false'
                            @add_plant_event='emiter($event)'/>
        </b-modal>
    </section>
</template>

<script>
import ModalFormPlant from './ModalFormPlant'

export default {
    name: 'ModalCreatePlant',
    props: ['cat_ids', 'user', 'url'],
    components: {
        ModalFormPlant
    },
    data: function() {
        return {
            category_id: this.cat_ids,
            credentials: this.user,
            URL: this.url,
            isComponentModalActive: false,
        }
    },
    methods: {
        emiter: function() {
            this.$emit('add_plant_event')
        }
    },
    beforeMount: function () {
        this.category_id = this.cat_id
    }
}
</script>