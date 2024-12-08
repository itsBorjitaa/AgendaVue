<template>
    <!-- microdata para formulario -->
    <section 
    id="nuevo" 
    itemscope 
    itemtype="http://schema.org/AddAction"
    >
    <div class="container">
        <div class="row">
        <div class="col-lg-12 text-center">
            <h2>Añadir contacto</h2>
            <hr class="star-primary">
        </div>
        </div>
        <div class="row">
        <div class="col-lg-8 col-lg-offset-2">
            <form @submit.prevent="submitContact">
            <div class="row control-group">
                <div class="form-group col-xs-12">
                <label>Nombre</label>
                <input 
                    type="text" 
                    class="form-control" 
                    placeholder="Nombre" 
                    v-model="name"
                    itemprop="agent" 
                    property="schema:name"
                    required
                >
                </div>
            </div>
            <div class="row control-group">
                <div class="form-group col-xs-12">
                <label>Email</label>
                <input 
                    type="email" 
                    class="form-control" 
                    placeholder="Email" 
                    v-model="email"
                    itemprop="recipient" 
                    property="schema:email"
                    required
                >
                </div>
            </div>
            <div class="row control-group">
                <div class="form-group col-xs-12">
                <label>Teléfono</label>
                <input 
                    type="tel" 
                    class="form-control" 
                    placeholder="Número de teléfono" 
                    v-model="phone"
                    itemprop="instrument" 
                    property="schema:telephone"
                    required
                >
                </div>
            </div>
            <br>
            <div class="row">
                <div class="form-group col-xs-12">
                <button 
                    type="submit" 
                    class="btn btn-success btn-lg"
                    itemprop="action"
                >
                    Añadir
                </button>
                </div>
            </div>
            </form>
        </div>
        </div>
    </div>
    </section>
</template>

<script>
import { ref } from 'vue'

export default {
    emits: ['add-contact'],
    setup(props, { emit }) {
    const name = ref('')
    const email = ref('')
    const phone = ref('')

    const submitContact = () => {
        if (name.value && email.value && phone.value) {
        emit('add-contact', {
            name: name.value,
            email: email.value,
            phone: phone.value
        })

        // resetear el formulario
        name.value = ''
        email.value = ''
        phone.value = ''
        }
    }

    return {
        name,
        email,
        phone,
        submitContact
    }
    }
}
</script>