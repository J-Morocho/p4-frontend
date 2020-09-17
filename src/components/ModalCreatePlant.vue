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
                            @close='isComponentModalActive = false'/>
        </b-modal>
    </section>
</template>

<script>
import ModalFormPlant from './ModalFormPlant'

export default {
    name: 'ModalCreatePlant',
    props: ['cat_id', 'user', 'url',],
    components: {
        ModalFormPlant
    },
    data: function() {
        return {
            isComponentModalActive: false,
            category_id: this.cat_id,
            credentials: this.user,
            URL: this.url
        }
    },
}
</script>