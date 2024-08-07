<template>
  <nav class="navbar" ref="navbar">
    <div class="logos">
      <img :src="govLogo" alt="Gobierno de Canarias Logo" class="partner-logo" />
      <img :src="ueLogo" alt="Unión Europea Logo" class="partner-logo partner-logo-hide" />
      <img :src="canariasLogo" alt="Canarias Avanza Logo" class="partner-logo partner-logo-hide" />
      <router-link to="/">
        <img :src="logo" alt="Logo del Proyecto" class="logo-img">
      </router-link>

    </div>
    <div class="menu-icon" @click="toggleMenu">
      <i class="fas fa-bars hamburger-icon"></i>
    </div>
    <ul :class="['nav-links', { 'nav-active': menuActive }]" @click.self="closeMenu">
      <li><router-link to="/" class="nav-item" :class="{ active: currentPage === 'inicio' }">INICIO</router-link></li>
      <li><router-link to="/restaurantes-solidarios" class="nav-item" :class="{ active: currentPage === 'restaurantes-solidarios' }">RESTAURANTES SOLIDARIOS</router-link></li>
      <li><router-link to="/proyecto" class="nav-item" :class="{ active: currentPage === 'proyecto' }">PROYECTO</router-link></li>
      <li><router-link to="/contacto" class="nav-item" :class="{ active: currentPage === 'contacto' }"> CONTACTO </router-link></li>
      <li><router-link to="/depto-comercial" class="nav-item departamento-comercial" :class="{ active: currentPage === 'departamento-comercial' }">DEPARTAMENTO COMERCIAL</router-link></li>
    </ul>
  </nav>
</template>


<script>
import logo from '@/assets/1.png';
import canariasLogo from '@/assets/fondos-europeos.png';
import ueLogo from '@/assets/union-europea.png';
import govLogo from '@/assets/Logo-Gobierno-de-Canarias-Consejeria-de-Economia-Conocimiento-y-Empleo-ACIISI-2-1.png';

export default {
  name: 'AppNavbar',
  props: {
    currentPage: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      logo,
      canariasLogo,
      ueLogo,
      govLogo,
      menuActive: false
    };
  },
  methods: {
    toggleMenu() {
      this.menuActive = !this.menuActive;
      if (this.menuActive) {
        document.addEventListener('click', this.handleClickOutside);
      } else {
        document.removeEventListener('click', this.handleClickOutside);
      }
    },
    closeMenu() {
      this.menuActive = false;
      document.removeEventListener('click', this.handleClickOutside);
    },
    handleClickOutside(event) {
      if (this.$refs.navbar && !this.$refs.navbar.contains(event.target)) {
        this.closeMenu();
      }
    }
  },
  beforeUnmount() {
    document.removeEventListener('click', this.handleClickOutside);
  }
};
</script>


<style scoped>
.navbar {
  display: flex;
  align-items: center;
  background-color: white;
  padding: 5px 15px;
  justify-content: space-between;
  width: 100%;
  box-sizing: border-box; /* Asegura que el padding se incluya en el ancho total */
}

.logos {
  display: flex;
  align-items: center;
}

.logo-img {
  max-width: 120px;
  max-height: 100px;
}

.partner-logo {
  max-width: 130px;
  max-height: 70px;
  margin-right: 20px;
}

.menu-icon {
  display: none; /* Oculto por defecto */
  cursor: pointer;
}

.hamburger-icon {
  font-size: 30px;
  color: #333;
}

.nav-links {
  list-style: none;
  display: flex;
  margin: 0;
  padding: 0;
}

.nav-item {
  display: block;
  padding: 10px 20px;
  margin-right: 10px;
  border-radius: 25px;
  color: white;
  text-decoration: none;
  font-size: 14px;
  font-weight: bold;
  background-color: #009EE3; /* Color azul por defecto */
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
  transition: box-shadow 0.3s ease;
}

.nav-item:hover {
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.3);
}

.nav-item.active {
  background-color: #001A66; /* Azul oscuro para la página actual */
}

.departamento-comercial {
  background-color: #9fdeeb; /* Azul muy claro para departamento comercial */
  color: black; /* Texto en negro para mejor contraste */
}

.departamento-comercial.active {
  background-color: black; /* Fondo negro para la página activa */
  color: white; /* Texto blanco para la página activa */
}

/* Estilos para el menú desplegable */
@media (max-width: 768px) {
  .logos {
    margin-left: 10px; /* Ajustar margen para pegar a la izquierda */
  }

  .nav-links {
    display: none;
    flex-direction: column;
    width: 80%; /* Ajustar el ancho del menú */
    text-align: left; /* Cambiar a la izquierda */
    position: absolute;
    top: 60px; /* Ajustar la posición del menú */
    left: 50%; /* Centrar horizontalmente */
    transform: translateX(-50%);
    background-color: white;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
    padding: 10px 0;
    z-index: 1;
  }

  .nav-links.nav-active {
    display: flex;
  }

  .menu-icon {
    display: block;
  }

  .nav-item {
    margin: 5px 0;
    padding: 10px;
    width: 100%;
    text-align: center;
  }

  .nav-item.departamento-comercial {
    background-color: #9fdeeb;
    color: black;
  }

  .nav-item.departamento-comercial.active {
    background-color: black; /* Fondo negro para la página activa */
    color: white; /* Texto blanco para la página activa */
  }

  .partner-logo-hide {
    display: none; /* Ocultar logos específicos en pantallas móviles */
  }
}
</style>
