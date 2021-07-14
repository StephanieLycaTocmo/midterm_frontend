<template>
    <div>
        <NavBar />
        <EditItemModal :item="selectedItem" />
        <DeleteItemModal :item="selectedItem" @onDeleted="getAll" />

        <div class="container">
            <h1>
                Items Entry
            </h1>
            
            <ItemEntryModal class="float-right mb-3" @onAdd="getAll" />

            <table class="table table-bordered table-striped">
                <thead>
                    <tr class="bg-dark text-white">
                        <th style="text-align:center">Name</th>
                        <th style="text-align:center">Description</th>
                        <th style="text-align:center">Price</th>
                        <th style="text-align:center">Quantity</th>
                        <th style="text-align:center">Condition</th>
                        <th style="text-align:center">&#x2713;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="item in items" :key="item.id">
                        <td style="text-align:center">{{item.name}}</td>
                        <td style="text-align:center">{{item.description}}</td>
                        <td style="text-align:center">{{item.price}}</td>
                        <td style="text-align:center">{{item.quantity}}</td>
                        <td style="text-align:center">{{item.condition}}</td>
                        <td class="buttons">
                            <b-button @click="onEdit(item)" variant="success" size="sm">
                                Edit
                            </b-button>
                            <b-button @click="onDelete(item)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            items: [],
            selectedItem: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('https://lentrix.tk/sltocmo/api/items')
            .then((res)=>{
                if (res.status==200) {
                    this.items = res.data
                };
            })
        },
        onEdit(selectedItem) {
            this.selectedItem = selectedItem
            this.$bvModal.show('editItemModal')
        },
        onDelete(selectedItem) {
            this.selectedItem = selectedItem
            this.$bvModal.show('deleteItemModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>

<style>
h1 {
    text-align: center;
    margin-top: 25px;
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}
.buttons {
    text-align: center;
}
</style>