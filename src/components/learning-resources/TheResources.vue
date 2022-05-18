<template>
  <base-card>
    <base-button
        @click="setSelectTab('stored-resources')"
        :mode="storedResButtonMode"
      >Stored Resources</base-button
    >
    <base-button 
        @click="setSelectTab('add-resource')" 
        :mode="addResButtonMode"
      >Add Resources</base-button
    >
  </base-card>
  <component :is="selectedTab"></component>
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
      resources: this.storedResources,
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resources' ? null : 'flat';
    },
  },
  methods: {
    setSelectTab(tab) {
      this.selectedTab = tab;
    },
  },
};
</script>

// note that the event listener is in the base-button element, which is NOT an
native html element. // However, by default, the event listenes falls through
the roof and go to the upper element, which in this case, // is a native button
element. So it works
