<template>
  <div class="bg-white rounded-lg shadow relative">
    <div class="grid grid-cols-6 gap-6 mt-5">
      {{ buttonkey }}
      <div class="col-span-3">
        <nestedList
          class="bg-gray-600 p-3"
          :list="linksMenu"
          @startDrag="startDrag($event[0], $event[1])"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import nestedList from "./components/_nestedList.vue";
import { ref } from "vue";

const linksMenu = ref([
  {
    order: 0,
    title: "Home",
    link: "/",
    children: [
      {
        title: "Quem Somos",
        link: "/quem-somos",
      },
      {
        title: "Missão Visão e Valores",
        link: "missao-visao-e-valores",
      },
      {
        title: "Organograma",
        link: "/organograma",
        children: [
          {
            title: "Testes",
            link: "/testes",
          },
        ],
      },
      {
        title: "Outro Teste",
        link: "outro-teste",
      },
    ],
  },
  {
    order: 1,
    title: "Sobre",
    link: "/sobre",
    children: [
      {
        title: "Contato",
        link: "/contato",
      },
    ],
  },
]);

const buttonkey = ref(0);

const startDrag = (evt, item) => {
  // console.log('startDrag')
  console.log("evt", evt);
  console.log("item", item);
  // console.log('titulo: ', evt.originalTarget.innerText)
  // evt.dataTransfer.dropEffect = 'move'
  // evt.dataTransfer.effectAllowed = 'move'
  // evt.dataTransfer.setData('itemID', item.id)
  // eslint-disable-next-line no-self-assign
  // linksMenu.value = linksMenu.value
  buttonkey.value = ++buttonkey.value;
};
</script>
