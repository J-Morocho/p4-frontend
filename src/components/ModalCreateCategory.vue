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
            
            <ModalFormCategory :user='credentials' :url='URL' @add_category_event='emiter($event)'/>
        </b-modal>
    </section>
</template>

<script>
import ModalFormCategory from './ModalFormCategory'

export default {
    name: 'ModalCreateCategory',
    props: ['user', 'url'],
    components: {
        ModalFormCategory
    },
    data: function() {
        return {
            isComponentModalActive: false,
            credentials: this.user,
            URL: this.url
        }
    },
    methods: {
        emiter: function(event) {
            this.$emit('add_category_event', event)
        }
    }
}

</script>