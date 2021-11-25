<template>
    <div>
        <form v-on:submit.prevent="validar">
            <div id="titulo">
                <h1>Validación de un formulario en Vue</h1>
            </div>
            <hr/>
            <div id="campos">
                <div>
                    <label>Nombre: </label>
                    <input type="text" id="nombre" v-model="nombre"/>
                    <div v-if="enviado && !$v.nombre.required" class="mensajeError">
                        Debe escribir un nombre.
                    </div>
                </div>
                <div>
                    <label>Edad: </label>
                    <input type="number" id="edad" v-model="edad"/>
                    <div v-if="enviado && !$v.edad.required" class="mensajeError">
                        Debe escribir una edad.
                    </div>
                </div>
                <div>
                    <label>Email: </label>
                    <input type="text" id="email" v-model="email"/>
                    <div v-if="enviado && !$v.email.required" class="mensajeError">
                        Debe escribir un email.
                    </div>
                    <div v-if="enviado && !$v.email.email" class="mensajeError">
                        Formato incorrecto.
                    </div>
                </div>
                <div>
                    <label>Contraseña: </label>
                    <input type="password" id="contraseña" v-model="contraseña"/>
                    <div v-if="enviado && !$v.contraseña.required" class="mensajeError">
                        Debe escribir una contraseña.
                    </div>
                    <div v-if="enviado && !$v.contraseña.minLength" class="mensajeError">
                        La contraseña debe contener mínimo 6 caracteres.
                    </div>
                </div>
                <div>
                    <label>Confirmar contraseña: </label>
                    <input type="password" id="confirmarContraseña" v-model="confirmarContraseña"/>
                    <div v-if="enviado && !$v.confirmarContraseña.required" class="mensajeError">
                        Debe escribir la confirmación de la contraseña.
                    </div>
                    <div v-if="enviado && !$v.confirmarContraseña.sameAsContraseña" class="mensajeError">
                        Las contraseñas deben coincidir.
                    </div>
                </div>
                <button>Validar</button>
            </div>
        </form>
    </div>
</template>

<script>
    import { required, email, minLength, sameAs } from 'vuelidate/lib/validators';
    export default {
        name: "Formulario",
        data(){
            return{
                nombre: "",
                edad: "",
                email: "",
                contraseña: "",
                confirmarContraseña: "",
                enviado: false
            }
        },
        validations: {
            nombre: { required },
            edad: { required },
            email: { required, email },
            contraseña: { required, minLength: minLength(6) },
            confirmarContraseña: { required, sameAsContraseña: sameAs("contraseña") }
        },
        methods: {
            validar(){
                this.enviado=true;
                // Si el formulario es inválido, no continúa.
                if (this.$v.$invalid) {
                    return;
                }
                console.log("Formulario válido.");
            }
        }
    }
</script>

<style scoped>
    form{
        width: fit-content;
        padding-top: 20px;
        border: 2px solid black;
        box-shadow: 6px 6px 12px 1px;
        border-radius: 20px;
        margin: 0 auto;
    }

    #titulo{
        padding: 0px 30px 0px 30px;
    }
    
    #campos{
        padding: 50px;
        text-align: left;
        margin-left: 70px;
    }

    button{
        margin-left: 35%;
        margin-top: 20px;
    }

    input{
        margin: 10px;
    }

    .mensajeError{
        color:rgb(230, 0, 0);
    }
</style>