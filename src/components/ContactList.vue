<template>
    <section id="contactos">
    <div class="container">
        <div class="row">
        <div class="col-lg-12 text-center">
            <h2>Contactos</h2>
            <hr class="star-primary">
        </div>
        </div>
        <div v-if="contacts.length === 0">
        <div class="row">
            <div class="col-xs-12">
            <p>No se ha encontrado ningún contacto.</p>
            </div>
        </div>
        </div>
        <div v-else>
        <div class="row">
            <div class="col-xs-4"><h4>Nombre</h4></div>
            <div class="col-xs-4"><h4>Email</h4></div>
            <div class="col-xs-3"><h4>Teléfono</h4></div>
        </div>
        <!-- microdata y rdfa para cada contacto -->
        <div 
            v-for="contact in contacts" 
            :key="contact.id" 
            class="row" 
            itemscope 
            itemtype="http://schema.org/Person"
            prefix="schema: http://schema.org/"
        >
            <div class="col-xs-4">
            <p>
                <span 
                itemprop="name" 
                property="schema:name"
                >
                {{ contact.name }}
                </span>
            </p>
            </div>
            <div class="col-xs-4">
            <p>
                <span 
                itemprop="email" 
                property="schema:email"
                >
                {{ contact.email }}
                </span>
            </p>
            </div>
            <div class="col-xs-3">
            <p>
                <span 
                itemprop="telephone" 
                property="schema:telephone"
                >
                {{ contact.phone }}
                </span>
            </p>
            </div>
            <div class="col-xs-1">
            <button 
                @click="$emit('delete-contact', contact.id)" 
                class="btn btn-danger btn-sm"
            >
                <span class="glyphicon glyphicon-remove"></span>
            </button>
            </div>
        </div>
        </div>
    </div>
    </section>
</template>

<script>
export default {
    props: {
    contacts: {
        type: Array,
        required: true
    }
    },
    emits: ['delete-contact']
}
</script>