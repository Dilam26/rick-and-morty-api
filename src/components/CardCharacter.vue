<template>
  <div class="character">
      <img :src="character.image" :alt="character.name">
      <div class="character__info">
          <h3>{{ character.name }}</h3>
          <div class="status">
              <span
                :class="
                    character.status == 'Alive' ? 'alive' :
                    character.status == 'Dead' ? 'dead' :
                    'default'
                "
              ></span>
              <span>{{ character.status }} - {{ character.species }}</span>
          </div>
          <div class="origin">
              <span>
                  Origin:
                  {{ character.origin.name }}
              </span>
          </div>
          <div class="location">
              Location:
              {{ character.location.name }}
          </div>
          <div class="container-btn">
              <button class="btn-modal" @click="$refs.modalName.openModal()">Ver mas</button>
          </div>
      </div>
  </div>

  <modal ref="modalName">
      <template v-slot:header>
        <h1></h1>
      </template>

      <template v-slot:body>
        <div class="contenido">
          <div class="img-content">
            <img :src="character.image" :alt="character.name">
          </div>
          <div class="info-content">
            <p>Id: {{ character.id }}</p>
            <p>Species: {{ character.species }}</p>
            <p>Gender: {{ character.gender }}</p>
            <p>Status: {{ character.status }}</p>
          </div>
        </div>
      </template>

      <template v-slot:footer>
        <div class="text-footer">
          <h1>{{ character.name }}</h1>
        </div>
      </template>
    </modal>
</template>

<script>
import Modal from './Modal.vue'
export default {
  components: { Modal },
    props: ['character']
}

</script>

<style lang="scss">
.character {
    background-color: var(--background-card);
    border-radius: 20px;
    box-shadow: 0 0 10px 1px var(--background-body);
    overflow: hidden;
    cursor: pointer;
    transition: transform 200ms ease-in-out;
    height: 100%;
    &:hover {
      transform: scale(1.05);
      h3{
        color: var(--text-orange);
        }
    }

    span {
      color: var(--text-gray);
    }

    h3{
      margin-bottom: 0.5rem;
    }
    &__info {
      padding: 1.5rem;
      .status {
        display: flex;
        align-items: center;
        margin-bottom: 0.5rem;
        span {
          color: var(--text-gray);
          &:first-child {
            width: 10px;
            height: 10px;
            border-radius: 50%;
          }
          &:last-child {
              margin-left: 8px;
          }
        }
        .alive {
          background-color: green;
        }
        .dead{
          background-color: red;
        }
        .default{
          background-color: #fff;
        }
      }
      .origin {
        margin-bottom: 0.5rem;
      }
      .container-btn{
        display: flex;
        justify-content: center;
      }
      .btn-modal {
        background-color: rgb(189, 188, 188);
        color: var(--background-card);
        margin-top: 1.5rem;
        padding: 0.5rem 2rem;
        border: none;
        text-transform: uppercase;
        border-radius: 20px;
        font-weight: bold;
        transition: .3s;
        &:hover {
          background-color: #fff;
          transform: translateY(-4px);
          transition: .3s;
          cursor: pointer;
        }
      }
    }
  }
  .contenido {
    margin-bottom: 15px;
    background: linear-gradient(to bottom, #323232 0%, #3F3F3F 40%, #1C1C1C 150%), linear-gradient(to top, rgba(255,255,255,0.40) 0%, rgba(0,0,0,0.25) 200%);
    background-blend-mode: multiply;
    color: #fff;
  }
  .info-content {
    padding: 5px;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    align-items: center;
    
    
    & p{
      padding: 5px 0;
      text-align: center;
      height: 100%;
      border: 1px solid rgb(189, 188, 188);

    }
}
</style>