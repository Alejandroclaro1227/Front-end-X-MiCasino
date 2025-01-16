<template>
    <div class="select-unselect-container">
        <div class="list">
            <h3>Available Options</h3>
            <ul>
                <li v-for="option in availableOptions" :key="option.id" @click="moveToDisabled(option)">
                    {{ option.label }}
                </li>
            </ul>
        </div>
        <div class="list">
            <h3>Disabled Options</h3>
            <ul>
                <li v-for="option in disabledOptions" :key="option.id" @click="moveToAvailable(option)">
                    {{ option.label }}
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: "SelectUnselectField",
    props: {
        field: {
            type: Object,
            required: true,
        },
        modelValue: {
            type: Object,
            default: () => ({ available: [], disabled: [] }),
        },
    },
    emits: ["update"],
    data() {
        return {
            availableOptions: [...this.modelValue.available],
            disabledOptions: [...this.modelValue.disabled],
        };
    },
    methods: {
        moveToDisabled(option) {
            this.availableOptions = this.availableOptions.filter(
                (item) => item.id !== option.id
            );
            this.disabledOptions.push(option);
            this.emitChange();
        },
        moveToAvailable(option) {
            this.disabledOptions = this.disabledOptions.filter(
                (item) => item.id !== option.id
            );
            this.availableOptions.push(option);
            this.emitChange();
        },
        emitChange() {
            this.$emit("update", {
                id: this.field.id,
                value: {
                    available: this.availableOptions,
                    disabled: this.disabledOptions,
                },
            });
        },
    },
};
</script>

<style scoped>
.select-unselect-container {
    display: flex;
    justify-content: space-around;
}

.list {
    width: 45%;
}

h3 {
    text-align: center;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    cursor: pointer;
    padding: 5px;
    margin: 5px 0;
    border: 1px solid #ccc;
    text-align: center;
}

li:hover {
    background-color: #f0f0f0;
}
</style>