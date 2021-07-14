<template>
    <div>
        <b-button v-b-modal.itemEntryModal variant="primary">Add Item</b-button>

        <b-modal id="itemEntryModal" title="Item Entry" ok-title="Save Item" @ok="onSubmit">
            <form action="#">
                <b-form-group label="Name" label-for="name">
                <b-form-input id="name" v-model="item.name" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Description" label-for="description">
                <b-form-input id="description" v-model="item.description" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Price" label-for="price">
                <b-form-input id="price" v-model="item.price" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Quantity" label-for="quantity">
                <b-form-input id="quantity" v-model="item.quantity" trim></b-form-input>
                </b-form-group>
                
                <b-form-group label="Condition" label-for="condition">
                <b-form-select v-model="item.condition" :options="options"></b-form-select>
                </b-form-group>

                <b-form-group label="Date Acquired" label-for="acquired_on">
                <b-form-input id="acquired_on" type="date" v-model="item.acquired_on" trim></b-form-input>
                </b-form-group>

            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    data() {
        return {
            item: {},
            options: [
                {value: 'good', text: 'New Stock'},
                {value: 'damaged', text: 'No defects'},
                {value: 'lost', text: 'Expired'},
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.post('https://lentrix.tk/sltocmo/api/items', this.item)
            .then((res)=>{
                if(res.status==202) {
                    alert('Successfully added an item')
                    this.$emit('onAdd')
                }
            });
        }
    }
}
</script>