<template>
  <div id="app">
    <ul>
      <li :class="{'active': tab.selected}" :key="tab.index" v-for="(tab, index) in tabs">
        <a href="#" @click.prevent="changeTab(index)">
          {{ tab.name }} 
          <i v-if="index != 0" @click.stop="removeTab(index)">X</i>
        </a>
      </li>
    </ul>
    <div id="tabList">
      <div :class="{'tabContent': true, 'active': tab.selected}" :key="tab.name" v-for="tab in tabs">
        <component :is="tab.componentName"></component>
      </div>
    </div>
  </div>
</template>

<script>
import HomePage from './components/HomePage';
import OtherPage from './components/OtherPage';
import AnotherPage from './components/AnotherPage';
import bus from './bus.js';

export default {
  name: 'App',
  components: {
    HomePage,
    OtherPage,
    AnotherPage
  },
  data () {
    return {
      tabs: [ 
        { name: 'Dashboard', componentName: 'HomePage', selected: true }
      ]
    }
  },
  mounted() {
    bus.$on('addTab', (tab) => {
      this.unSelectTabs();
      tab.selected = true;
      this.tabs.push(tab);
    });    
  },
  methods: {
    unSelectTabs: function () {
      this.tabs.forEach(currentTab => currentTab.selected = false);
    },
    changeTab: function (tab)  {
      this.tabs.forEach(currentTab => currentTab.selected = false);
      this.tabs[tab].selected = true;
    },
    removeTab(tab) {
      this.tabs.splice(tab, 1);
      this.unSelectTabs();
      this.changeTab(0);
    }
  }
}
</script>

<style>
ul li { display: inline; padding: 2px;  margin: 2px; }
ul li a { text-decoration: none; }
li.active { border-bottom: solid 3px cyan; }
.tabContent { display: none; padding: 2px;  margin: 2px;}
.tabContent.active { display: block;}
</style>
