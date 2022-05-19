<template>
  <base-card>
    <base-button
      @click="setSelectTab('stored-resources')"
      :mode="storedResButtonMode"
      >Stored Resources</base-button
    >
    <base-button @click="setSelectTab('add-resource')" :mode="addResButtonMode"
      >Add Resources</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResources.vue';
export default {
  components: {
    StoredResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.com',
        },
      ],
    };
  },
  provide() {
    return {
      addResource: this.addResource,
      resources: this.storedResources,
      removeResource: this.removeResource
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  methods: {
    setSelectTab(tab) {
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
    removeResource(resID) {
      const resIndex = this.storedResources.findIndex(res => res.id === resID);
      this.storedResources.splice(resIndex, 1);
    }
  },
};
</script>

// note that the event listener is in the base-button element, which is NOT an
native html element. // However, by default, the event listenes falls through
the roof and go to the upper element, which in this case, // is a native button
element. So it works
