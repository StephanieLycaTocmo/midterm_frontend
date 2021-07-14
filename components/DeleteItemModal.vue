<template>
    <div>
        <b-modal id="deleteItemModal" title="Delete item" ok-title="Delete item" @ok="onDelete" ok-variant="danger">
            Are you sure in deleting this item? <br><br>
            Name: {{item.name}} <br>
            Description: {{item.description}}
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        item: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('https://lentrix.tk/sltocmo/api/items/' + this.item.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Deleted successfully!')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>