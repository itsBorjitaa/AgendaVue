<template>
  <nav class="navbar navbar-default navbar-fixed-top">
    <div class="container">
      <div class="navbar-header page-scroll">
        <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1">
          <span class="sr-only">Cambiar navegación</span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
        </button>
        <a class="navbar-brand" href="#page-top">AgendaVue</a>
      </div>
      <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
        <ul class="nav navbar-nav navbar-right">
          <li class="page-scroll">
            <a href="#contactos">Contactos</a>
          </li>
          <li class="page-scroll">
            <a href="#nuevo">Añadir contacto</a>
          </li>
          <li class="page-scroll">
            <a href="#about">Acerca de...</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <header>
    <div class="container">
      <div class="row">
        <div class="col-lg-12">
          <div class="intro-text">
            <span class="name">AgendaVue</span>
            <hr class="star-light">
            <span class="skills">Agenda básica en Vue 3</span>
          </div>
        </div>
      </div>
    </div>
  </header>

  <ContactList 
    :contacts="contacts" 
    @delete-contact="deleteContact"
  />
  
  <ContactForm @add-contact="addContact" />
  
  <AboutSection />

  <footer class="text-center">
    <div class="footer-below">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            Copyleft &copy; e-ghost 2024
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import { ref, onMounted } from 'vue'
import ContactList from './components/ContactList.vue'
import ContactForm from './components/ContactForm.vue'
import AboutSection from './components/AboutSection.vue'

export default {
  components: {
    ContactList,
    ContactForm,
    AboutSection
  },
  setup() {
    const contacts = ref([
      {
        id: 1,
        name: 'John Doe',
        email: 'john.doe@deusto.es',
        phone: '555555555'
      }
    ])

    // función para generar el JSON-LD
    const generateJsonLd = () => {
      const jsonLdScript = document.createElement('script')
      jsonLdScript.type = 'application/ld+json'
      jsonLdScript.textContent = JSON.stringify({
        "@context": "https://schema.org",
        "@type": "ContactList",
        "name": "AgendaVue Contactos",
        "numberOfItems": contacts.value.length,
        "itemListElement": contacts.value.map(contact => ({
          "@type": "Person",
          "name": contact.name,
          "email": contact.email,
          "telephone": contact.phone
        }))
      })
      document.head.appendChild(jsonLdScript)
    }

    const addContact = (contact) => {
      contact.id = contacts.value.length + 1
      contacts.value.push(contact)
      // regenerar el json al añadir contacto
      generateJsonLd()
    }

    const deleteContact = (contactId) => {
      contacts.value = contacts.value.filter(contact => contact.id !== contactId)
      // regenerar el json al eliminar contacto
      generateJsonLd()
    }

    // generar el json al montar la aplicación
    onMounted(generateJsonLd)

    return {
      contacts,
      addContact,
      deleteContact
    }
  }
}
</script>