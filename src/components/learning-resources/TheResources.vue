<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButtonMode"
    >
      Stored Resources</base-button
    >
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
      >Add Resources</base-button
    >
    <base-button
      @click="setSelectedTab('resource-history')"
      :mode="addHistoryButtonMode"
      >History</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>


<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';
import ResourceHistory from './ResourceHistory.vue';

export default {
  components: {
    StoredResources,
    AddResource,
    ResourceHistory,
  },

  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official vue.js documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google',
          link: 'https://google.org',
        },
      ],
      deletedResources: [],
    };
  },

  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.removeResource,
      deletedResources: this.deletedResources,
    };
  },

  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
    addHistoryButtonMode() {
      return this.selectedTab === 'resource-history' ? null : 'flat';
    },
  },

  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url,
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },
    removeResource(resId) {
      const resIndex = this.storedResources.findIndex(
        (res) => res.id === resId
      );
      const deletedResource = this.storedResources.splice(resIndex, 1)[0];
      this.deletedResources.unshift(deletedResource);
    },
  },
};
</script>
