<template>
    <div class="select-unselect-container">
        <div class="options-grid">
            <div class="options-column">
                <div class="column-header">Available Options</div>
                <div class="options-box">
                    <div v-for="option in availableOptions" 
                         :key="option.id" 
                         @click="toggleOption(option)"
                         class="option-item">
                        {{ option.label }}
                    </div>
                </div>
            </div>
            <div class="options-column">
                <div class="column-header">Disabled options</div>
                <div class="options-box">
                    <div v-for="option in disabledOptions" 
                         :key="option.id" 
                         @click="toggleOption(option)"
                         class="option-item">
                        {{ option.label }}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'SelectUnselectField',
    props: {
        field: {
            type: Object,
            required: true
        },
        modelValue: {
            type: Array,
            default: () => []
        }
    },
    computed: {
        availableOptions() {
            return this.field.options.filter(opt => opt.status === 'Available');
        },
        disabledOptions() {
            return this.field.options.filter(opt => opt.status === 'Disabled');
        }
    },
    methods: {
        toggleOption(selectedOption) {
            // Solo cambiamos el estado de la opción seleccionada
            const updatedOptions = this.field.options.map(option => {
                if (option.id === selectedOption.id) {
                    return {
                        ...option,
                        status: option.status === 'Available' ? 'Disabled' : 'Available'
                    };
                }
                return option;
            });

            // Actualizamos las opciones en el campo
            this.field.options = updatedOptions;

            // Emitimos el evento con las opciones actualizadas
            this.$emit('update', {
                id: this.field.id,
                value: updatedOptions.filter(opt => opt.status === 'Disabled').map(opt => opt.id)
            });
        }
    }
};
</script>

<style scoped>
.select-unselect-container {
    width: 100%;
}

.options-grid {
    display: flex;
    gap: 20px;
}

.options-column {
    flex: 1;
}

.column-header {
    color: white;
    text-align: left;
    margin-bottom: 5px;
}

.options-box {
    background-color: #000;
    border: 1px solid #333;
    border-radius: 4px;
    min-height: 120px;
    padding: 10px;
}

.option-item {
    color: white;
    padding: 8px;
    cursor: pointer;
    border-bottom: 1px solid #333;
    text-align: left;
}

.option-item:hover {
    background-color: #333;
}
</style> 