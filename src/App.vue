<template>
  <h1 class="roadmap sfProDisplay">Roadmap</h1>
  <a class="isaac sfProText400" href="https://www.isaacnc.com/" target="_blank">By Isaac N.C. Visit website</a>
  
  <div class="backlog mainContainers"
  @drop="onDrop($event, 1)"
  @dragenter.prevent
  @dragover.prevent
  >
    <a class="sfProDisplayH3">Backlog</a>
    <div v-for="item in getList(1)" 
    :key="item.id" 
    class="drag-el sfProText600"
    draggable="true"
    @dragstart="startDrag($event, item)"
    >
    {{ item.title }}
      <div class="sfProText400">
        {{item.text}}
      </div>
    </div>
  </div>

  <div class="toDo mainContainers"
  @drop="onDrop($event, 2)"
  @dragenter.prevent
  @dragover.prevent
  >
    <a class="sfProDisplayH3">To do</a>
    <div v-for="item in getList(2)" 
    :key="item.id" 
    class="drag-el sfProText600"
    draggable="true"
    @dragstart="startDrag($event, item)"
    >
    {{ item.title }}
    <div class="sfProText400">
        {{item.text}}
      </div>
    </div>
  </div>

  <div class="inProgress mainContainers"
  @drop="onDrop($event, 3)"
  @dragenter.prevent
  @dragover.prevent
  >
    <a class="sfProDisplayH3">In progress</a>
    <div v-for="item in getList(3)" 
    :key="item.id" 
    class="drag-el sfProText600"
    draggable="true"
    @dragstart="startDrag($event, item)"
    >
    {{ item.title }}
    <div class="sfProText400">
        {{item.text}}
      </div>
    </div>
  </div>

  <div class="designed mainContainers"
  @drop="onDrop($event, 4)"
  @dragenter.prevent
  @dragover.prevent
  >
    <a class="sfProDisplayH3">Designed</a>
    <div v-for="item in getList(4)"
    :key="item.id" 
    class="drag-el sfProText600"
    draggable="true"
    @dragstart="startDrag($event, item)"
    >
    {{ item.title }}
      <div class="sfProText400">
          {{item.text}}
      </div>
    </div>
  </div>

<div>
</div>
</template>

<script>
  import { ref } from 'vue'

  export default {
    setup(){
      const items = ref([
        {id : 0, title: 'Twilio integration', text: 'Create new note via SMS. Support text, audio, links, and media.' , list: 1},
        {id : 1, title: 'Markdown support', text: 'Markdown shorthand converts to formatting', list: 1},
        {id : 2, title: 'Tablet view', text: '', list: 2},
        {id : 3, title: 'Audio recording in note', text: 'Show audio in a note and playback UI', list: 2},
        {id : 4, title: 'Bookmark in note', text: 'Show rich link UI in a note, and feature to render website screenshot.', list: 2},
        {id : 5, title: 'Image viewer', text: 'Opens when clicking on the thumbnail in the list or on the image in the note', list: 2},
        {id : 6, title: 'Mobile view', text: 'Functions for both web responsive and native apps. Note: Android and iOS will need unique share icons.', list: 3},
        {id : 7, title: 'Desktop view', text: 'PWA for website and native apps. Note: Windows and Mac will need unique share icons.', list: 3},
        {id : 8, title: 'Formatting options', text: 'Mobile formatting bar expands and collapses when tapping the format icon.', list: 3},
        {id : 9, title: 'Media in note', text: 'Image & video with player UI', list: 3},
        {id : 10, title: 'Audio recording', text: 'Interface for when recording a new audio note', list: 4},
        {id : 11, title: 'Bookmarking', text: 'Interface for when creating a new link note.', list: 4},
        {id : 12, title: 'Mobile home screen', text: 'Folders, tags, and notes lists are sorted by recent.', list: 4},
      ])

      const getList = (list) => {
        return items.value.filter((item) => item.list == list)
      }

      const startDrag = (event, item) =>{
        event.dataTransfer.dropEffect = 'move'
        event.dataTransfer.effectAllowed = 'move'
        event.dataTransfer.setData('itemID', item.id)
      }

      const onDrop = (event, list) => {
        const itemID = event.dataTransfer.getData('itemID')
        const item = items.value.find((item) => item.id == itemID)
        item.list = list
      }

      return{
        getList,
        onDrop,
        startDrag,
      }
    }
  }
</script>


<style>

  body{
    max-width: 1920px;
    max-height: 1080px;
    background: #000000;
  }

  .roadmap{
    position: absolute;
    height: 60px;
    font-size: 50px;
    line-height: 60px;
    top: 89px;
    left: 224px;
  }

  .isaac{
    top: 190px;
    left: 224px;
    position:absolute;
  }

  .backlog{
    left: 200px; 
    position: absolute;
  }
  .toDo{
    left: 600px;
    position: absolute;
  }
  .inProgress{
    left: 1000px;
    position: absolute;
  }
  .designed{
    left: 1400px;
    position: absolute;
  }

  
  .mainContainers{
    display: flex;
    flex-direction: column;
    align-items: left;
    padding: 24px;
    gap: 16px;
    min-height: 100px;
    width: 344px;
    background: #262626;
    border-radius: 16px;
    top: 240px;
  }

  .drag-el{
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    padding: 24px;
    gap: 8px;

    width: 296px;
    min-height: 30px;
    
    background: #D93535;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.12), 0px 16px 32px rgba(0, 0, 0, 0.08);
    border-radius: 8px;

    flex: none;
    order: 1;
    flex-grow: 0;
  }

  .sfProDisplay{
    font-family: 'SF Pro Display';
    font-style: normal;
    font-weight: 700;
    color: #ffffff;
  }

  .sfProDisplayH3{
    font-family: 'SF Pro Display';
    font-style: normal;
    font-weight: 700;
    font-size: 37px;
    line-height: 44px;
    color: #ffffff;
  }

  .sfProText600{
    font-family: 'SF Pro Text';
    font-style: normal;
    font-weight: 600;
    font-size: 16px;
    line-height: 150%;
    color: #ffffff;
  }

  .sfProText400{
    font-family: 'SF Pro Text';
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 140%;
    color: rgba(255, 255, 255, 0.75);
  }

</style>