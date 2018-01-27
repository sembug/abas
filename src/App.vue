<template>
  <div id="app">
    <ul>
      <li :class="{'active': tab.selected}" :key="tab.index" v-for="tab in tabs">
        <a href="#" @click.prevent="changeTab(tab.index)">
          {{ tab.name }} 
          <i v-if="tab.index != 0" @click.stop="removeTab(tab.index)">X</i>
        </a>
      </li>
    </ul>
    <div id="tabList">
      <div :class="{'tabContent': true, 'active': tab.selected}" :key="tab.index" v-for="tab in tabs">
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
      activeTab: 0,
      indexControl: 0,
      tabs: [ 
        { index: 0, name: 'Dashboard', componentName: 'HomePage', selected: true }
      ]
    }
  },
  mounted() {
    bus.$on('addTab', (tab) => {
      this.indexControl += 1;
      tab.index = this.indexControl;
      for (var i = 0; i < this.tabs.length; i++) {
        this.tabs[i].selected = (this.tabs[i].index == -1);
      }
      tab.selected = true;
      this.tabs.push(tab);
    });    
  },
  methods: {
    changeTab: function (tab)  {
      for (var i = 0; i < this.tabs.length; i++) {
        this.tabs[i].selected = (this.tabs[i].index == tab);
      }
    },
    removeTab(tab) {
      var newTabs = this.tabs.filter(item => {
        return item.index != tab;
      });

      for (var i = 0; i < newTabs.length; i++) {
        newTabs[i].selected = (newTabs[i].index == 0);         
      }

      console.log(newTabs[0].selected);
      this.tabs = newTabs;
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
