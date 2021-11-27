<template>
  <div class="interfaces">
    <div class="card-wrapper">
      <div class="card" v-for="ifc of interfaces" :key="ifc.name">
        <div class="header">
          <span class="name">{{ ifc.name }}</span>
          <span class="health-details__status" v-bind:class="[ifc.up ? 'health-details__status--UP' : 'health-details__status--DOWN']">
            {{ ifc.up ? 'UP' : 'DOWN' }}
          </span>
        </div>
        <p class="description">{{ ifc.description }}</p>
        <div class="actions">
          <a href="#">Documentation</a>
          <a href="#">Manage interface definitions</a>
        </div>
        <div class="tags">
          <div class="tag" v-for="tag of ifc.tags" :key="tag">{{ tag }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      instance: { //<1>
        type: Object,
        required: true
      }
    },
    data: () => ({
      interfaces: ''
    }),
    async created() {
      const response = await this.instance.axios.get('actuator/interfaces'); //<2>
      this.interfaces = response.data;
    }
  };
</script>

<style>
  .interfaces {
    font-size: 20px;
    width: 80%;
    padding: 20px;
  }
  .interfaces .card-wrapper {
    display: flex;
  }
  .interfaces .card {
    width: 600px;
    padding: 20px;
    margin-right: 10px;
  }
  .interfaces .card .header {
    font-weight: bold;
  }
  .interfaces .card .name {
    font-size: 200%;
  }
  .interfaces .card .actions {
    font-size: 80%;
    padding: 10px 0;
  }
  .interfaces .card .actions a {
    display: block;
  }
  .interfaces .card .tags {
    padding: 10px 0;
  }


  /* TODO: these style don't really belong to this custom view. They are here to help styling the whole
      application. We need to find another place for them.
   */
  .navbar {
    background-color: #f3f4f7 !important;
  }
  .navbar-item {
    color: black !important;
  }

  .navbar a:hover {
    background-color: white !important;
    color: #0ba6ff !important;
  }

  .navbar-item .is-active a {
    background-color: white !important;
    color: #0ba6ff !important;
  }

  .navbar-link {
    color: black !important;
  }

  a.navbar-item.is-active:not(:focus):not(:hover) {
    background-color: white !important;
    color: #0ba6ff !important;
  }

  a.navbar-item.is-active, a.navbar-item:focus, a.navbar-item:focus-within, a.navbar-item:hover {
    background-color: white !important;
    color: #0ba6ff !important;
  }

  .navbar-link:not(.is-arrowless):after {
    border-color: #0ba6ff !important;
  }

  .sidebar {
    background-color: #00507d !important;
  }

  .sidebar .instance-summary {
    background-color: #0ba6ff !important;
  }

  /*.sidebar .instance-summary--UP {
    background-color: #0ba6ff !important;
  }*/
  .is-active {
    color: white !important;
  }
  .sidebar .sidebar-group.is-active .sidebar-group-items a.is-active {
    background-color: #0078BD !important;
  }

  .sidebar .sidebar-group.is-active .sidebar-group-items a:hover {
    background-color: #0ba6ff !important;
  }

  .sidebar .sidebar-group.is-active {
    box-shadow: inset 4px 0 0 white !important;
  }

  .sidebar a {
    color: white !important;
  }

  .sidebar a:hover {
    color: white !important;
  }

  .tag:not(body).is-primary {
    background-color: #0ba6ff !important;
  }

  .hex.is-primary polygon {
    fill: #0078bd !important;
    stroke: #0078bd !important;
  }

  .button.is-primary {
    background-color: #0078BD !important;
  }

  .button .is-primary :hover {
    background-color: #0ba6ff !important;
  }

  .health-details__status--UP {
    color: #0078bd !important;
  }

  .application-status__icon--UP {
    color: #0078bd !important;
  }

  .has-text-success {
    color: #0078bd !important;
  }

  .login {
    background-color: #880000 !important;
    /*background-image: url("/assets/img/background.png") !important;*/
  }

  .hero.is-primary {
    background-color: #0078bd !important;
  }

  .has-text-primary {
    background-color: #0078bd !important;
  }

  a {
    color: #0078bd !important;
  }

  a:hover {
    color: #0ba6ff !important;
  }
</style>

