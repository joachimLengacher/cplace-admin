<!--
  - Copyright 2014-2018 the original author or authors.
  -
  - Licensed under the Apache License, Version 2.0 (the "License");
  - you may not use this file except in compliance with the License.
  - You may obtain a copy of the License at
  -
  -     http://www.apache.org/licenses/LICENSE-2.0
  -
  - Unless required by applicable law or agreed to in writing, software
  - distributed under the License is distributed on an "AS IS" BASIS,
  - WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  - See the License for the specific language governing permissions and
  - limitations under the License.
  -->

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
</style>

