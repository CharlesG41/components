<template>
    <div>
        <div 
            class="drop-zone" 
            @drop="onDrop($event, 1)"
            @dragover.prevent
            @dragenter.prevent
        >
            <div 
                class="flex" 
                v-for="item in listOne" 
                :key="item.title"
            >
                <div
                    class="px-4 py-2 bg-gray-100 cursor-move"
                    draggable="true"
                    @dragstart="startDrag($event, item)"
                >
                    {{ item.id }}
                </div>
                <div class="w-full bg-white py-2">
                    {{ item.title }}
                </div>
            </div>
        </div>
        <div 
            class="drop-zone"
            @drop="onDrop($event, 2)"
            @dragover.prevent
            @dragenter.prevent
        >
            <div 
                class="flex" 
                v-for="item in listTwo" 
                :key="item.title"
            >
                <div
                    class="px-4 py-2 bg-gray-100 cursor-move"
                    draggable="true"
                    @dragstart="startDrag($event, item)"
                >
                    {{ item.id }}
                </div>
                <div class="w-full bg-white py-2">
                    {{ item.title }}
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            items: [
                {
                    id: 0,
                    title: 'Item A',
                    list: 1,
                },
                {
                    id: 1,
                    title: 'Item B',
                    list: 1,
                },
                {
                    id: 2,
                    title: 'Item C',
                    list: 2,
                },
            ],
        }
    },
    methods: {
        startDrag(evt, item) {
            console.log('startDrag')
            evt.dataTransfer.dropEffect = 'move'
            evt.dataTransfer.effectAllowed = 'move'
            evt.dataTransfer.setData('itemID', item.id)
        },
        onDrop(evt, list) {
            console.log('onDrop')
            const itemID = evt.dataTransfer.getData('itemID')
            const item = this.items.find((item) => item.id == itemID)
            item.list = list
        },
    },
    computed: {
        listOne() {
            return this.items.filter((item) => item.list === 1)
        },
        listTwo() {
            return this.items.filter((item) => item.list === 2)
        },
    },
}
</script>

<style scoped>
.drop-zone {
  background-color: #eee;
  margin-bottom: 10px;
  padding: 10px;
}
.drag-el {
  background-color: #fff;
  margin-bottom: 10px;
  padding: 5px;
}
</style>