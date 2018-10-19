<template>
  <div>
    <div class="components">
      <div class="components-list">
        <draggable v-model="pages">
          <transition-group name="list-complete" type="transition">
            <div v-for="(page, index) in pages" :key="page.order" class="component-list-item">
              <div class="component-list-item" @click="showComponent(index)" v-if="page.name === 'hero'">
                <h2>Hero</h2>
                <a href="#" @click="removeItem(index)">remover</a>
              </div>
              <div class="component-list-item" @click="showComponent(index)" v-if="page.name === 'modules'">
                <h2>Módulo com carrossel de vídeos</h2>
                <a href="#" @click="removeItem(index)">remover</a>
              </div>
              <div class="component-list-item" @click="showComponent(index)" v-if="page.name === 'tasting'">
                <h2>Prova do vídeo</h2>
                <a href="#" @click="removeItem(index)">remover</a>
              </div>
              <div class="component-list-item" @click="showComponent(index)" v-if="page.name === 'testimonials'">
                <h2>Depoimentos</h2>
                <a href="#" @click="removeItem(index)">remover</a>
              </div>
              <div class="component-list-item" @click="showComponent(index)" v-if="page.name === 'cta'">
                <h2>Call to action</h2>
                <a href="#" @click="removeItem(index)">remover</a>
              </div>
            </div>
          </transition-group>
        </draggable>

        <button @click="addComponent()">
          Adicionar Component
        </button>
      </div>

      <div class="components-page">
        <div v-if="showComponentList">
          <h1 @click="addItem('hero')">Hero</h1>
          <h1 @click="addItem('modules')">Módulo</h1>
          <h1 @click="addItem('tasting')">Prova do vídeo</h1>
          <h1 @click="addItem('testimonials')">Depoimentos</h1>
          <h1 @click="addItem('cta')">Call to action</h1>
        </div>

        <div v-if="showComponentInfos">
          <div v-if="pages[activeIndex].name === 'hero'">
            <h2>Hero</h2>
            <label for="">
              Título
              <input type="text" v-model="pages[activeIndex].title">
            </label>

            <label for="">
              Descrição
              <textarea type="text" v-model="pages[activeIndex].description"></textarea>
            </label>

            <label for="">
              Label do botão
              <input type="text" v-model="pages[activeIndex].button">
            </label>

            <label for="">
              Link do botão
              <input type="text" v-model="pages[activeIndex].link">
            </label>

            <a href="#" @click="removeItem(activeIndex)">Remover</a>
          </div>

          <div v-if="pages[activeIndex].name === 'modules'">
            <h2>Módulo com carrossel de vídeos</h2>

            <label for="">
              Título
              <input type="text" v-model="pages[activeIndex].title">
            </label>

            <a href="#" @click="removeItem(activeIndex)">Remover</a>
          </div>

          <div v-if="pages[activeIndex].name === 'tasting'">
            <h2>Prova do vídeo</h2>

            <label for="">
              Título
              <input type="text" v-model="pages[activeIndex].title">
            </label>

            <a href="#" @click="removeItem(activeIndex)">Remover</a>
          </div>

          <div v-if="pages[activeIndex].name === 'testimonials'">
            <h2>Depoimentos</h2>

            <label for="">
              Título
              <input type="text" v-model="pages[activeIndex].title">
            </label>

            <a href="#" @click="removeItem(activeIndex)">Remover</a>
          </div>

          <div v-if="pages[activeIndex].name === 'cta'">
            <h2>Call to action</h2>

            <label for="">
              Título
              <input type="text" v-model="pages[activeIndex].title">
            </label>

            <a href="#" @click="removeItem(activeIndex)">Remover</a>
          </div>
        </div>
      </div>
    </div>
    
    <div class="btn-list">
      <button class="btn-save" @click="savePage()">Salvar</button>
    </div>

    <div class="result">
      <pre>{{componentList}}</pre>
    </div>
  </div>
</template>

<script>

import draggable from 'vuedraggable'

export default {
  name: 'Components',

  components: {
    draggable,
  },

  data () {
    return {
      pages: [],
      componentList: '',
      showComponentList: false,
      activeIndex: 0,
      showComponentInfos: false,
    }
  },

  methods: {
    addComponent() {
      this.showComponentList = true;
    },

    showComponent(index) {
      console.log(index)
      this.activeIndex = index;
      this.showComponentInfos = true;
    },

    savePage() {
      this.componentList = this.pages;
      console.log(JSON.stringify(this.pages))
    },

    addItem(component) {
      const order = this.pages.length + 1;

      if (component === 'hero') {
        this.pages.push({
          order: order,
          name: 'hero',
          title: '',
          description: '',
          button: '',
          link: '',
        })
      }

      if (component === 'modules') {
        this.pages.push({
          order: order,
          name: 'modules',
          title: '',
        })
      }

      if (component === 'tasting') {
        this.pages.push({
          order: order,
          name: 'tasting',
          title: '',
        })
      }

      if (component === 'testimonials') {
        this.pages.push({
          order: order,
          name: 'testimonials',
          title: '',
        })
      }

      if (component === 'cta') {
        this.pages.push({
          order: order,
          name: 'cta',
          title: '',
        })
      }

      this.showComponentList = false;
    },

    removeItem(index) {
      this.pages.splice(index, 1);
    },
  }
}
</script>

<style lang="scss">
  @import 'comp.scss';
</style>
