<script lang="ts">

/*
Este código é um componente Vue que define um campo de entrada personalizado com um ícone.
Ele espera receber algumas propriedades (como icon, alt, name, type, placeholder e modelValue) 
e possui métodos para manipular o estado de foco do input e uma propriedade computada para vincular o valor do input.
*/


    // Importa a função defineComponent do Vue para definir um novo componente
    import { defineComponent } from 'vue';

    // Exporta o componente padrão definido com Vue
    export default defineComponent({
        // Define as propriedades esperadas pelo componente
        props:{
            icon: String, // Propriedade para o ícone (espera uma string)
            alt: String, // Propriedade para o texto alternativo do ícone (espera uma string)
            name: String, // Propriedade para o nome do input (espera uma string)
            type: String, // Propriedade para o tipo do input (espera uma string)
            placeholder: String, // Propriedade para o placeholder do input (espera uma string)
            modelValue: String, // Propriedade para o valor do input (espera uma string)
        },
        // Define o estado de dados do componente
        data(){
            return {
                inputFocus: false // Inicializa o estado de foco do input como falso
            }
        },
        // Define métodos personalizados para o componente
        methods:{
            // Método para definir o estado de foco do input
            setFocus(v: boolean){
                this.inputFocus = v; // Define o estado de foco com base no valor passado
            }
        },
        // Define propriedades computadas do componente
        computed:{
            // Propriedade computada para o modelo do input
            model:{
                // Getter: retorna o valor do modelo
                get(){
                    return this.modelValue; // Retorna o valor do modelo
                },
                // Setter: define o valor do modelo e emite um evento 'setInput'
                set(v:any){
                    this.$emit('setInput', v); // Emite um evento 'setInput' com o novo valor
                }
            }
        }
    });
</script>

<template>
    <!-- Template do componente -->
    <div class="input" :class="{ focus: inputFocus }"> <!-- Div principal do input -->
        <img :src="icon" :alt="alt" /> <!-- Exibe o ícone -->
        <input :type="type" :name="name" :placeholder="placeholder" 
            v-model="model"
            @focus="setFocus(true)" 
            @blur="setFocus(false)"/> <!-- Define o estado de foco como falso ao desfocar do input -->
    </div>
</template>
