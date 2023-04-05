<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <p>this is start ...</p>
  <div>
    <BlitzForm v-model="formData" :schema="makejson(jsonSchema)" :columnCount="2"/>

    <CodeBlock :content="`// formData\n${JSON.stringify(formData, undefined, 2)}`"/>
  </div>
  <p>this is end ...</p>
</template>

<script setup>
import {BlitzForm} from 'blitzar'
// include Blitzar's CSS (kept at minimal and doesn't pollute global scope)
import 'blitzar/dist/style.css'
// import HelloWorld from './components/HelloWorld.vue'
import {ref} from 'vue'

// eslint-disable-next-line no-unused-vars
const jsonSchema = `{
  "definitions": {},
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "https://example.com/object1677406192.json",
  "title": "Root",
  "type": "object",
  "required": [
    "downloadURL",
    "buildNumber",
    "versionName",
    "type",
    "changeLog"
  ],
  "properties": {
    "downloadURL": {
      "$id": "#root/downloadURL",
      "title": "Downloadurl",
      "type": "string",
      "default": "",
      "examples": [
        "itms-services://?action=download-manifest&url=https://taraapp.s3.ir-thr-at1.arvanstorage.com/club.plist"
      ],
      "pattern": "^.*$"
    },
    "buildNumber": {
      "$id": "#root/buildNumber",
      "title": "Buildnumber",
      "type": "integer",
      "examples": [
        152
      ],
      "default": 0
    },
    "versionName": {
      "$id": "#root/versionName",
      "title": "Versionname",
      "type": "string",
      "default": "",
      "examples": [
        "1.18.2"
      ],
      "pattern": "^.*$"
    },
    "type": {
      "$id": "#root/type",
      "title": "Type",
      "type": "string",
      "default": "",
      "examples": [
        "optional"
      ],
      "pattern": "^.*$"
    },
    "changeLog": {
      "$id": "#root/changeLog",
      "title": "Changelog",
      "type": "array",
      "default": [],
      "items":{
        "$id": "#root/changeLog/items",
        "title": "Items",
        "type": "string",
        "default": "",
        "examples": [
          ";dvاز تارالند!"
        ],
        "pattern": "^.*$"
      }
    }
  }
}`;
// eslint-disable-next-line no-unused-vars
const schema = [
  {
    id: 'name',
    span: 1,
    component: 'input',
    label: 'Superhero name',
    subLabel: 'Think of something cool.',
    required: true,
  },
  {
    id: 'powerOrigin',
    label: 'Power origin',
    subLabel: 'Where does your power come from?',
    // component props:
    component: 'select',
    slot: [
      {component: 'option', value: '', slot: 'Select one', disabled: true},
      {component: 'option', value: 'mutation', slot: 'Mutation'},
      {component: 'option', value: 'self', slot: 'Self taught'},
      {component: 'option', value: 'item', slot: 'Magic item'},
      {component: 'option', value: 'gear', slot: 'Gear'},
    ],
  },
  {
    id: 'stamina',
    span: 2,
    component: 'input',
    type: 'range',
    label: 'Stamina',
    subLabel: (value) => `value: ${value}`,
    dynamicProps: ['subLabel'],
    parseInput: (val) => Number(val),
    defaultValue: 50,
    min: 0,
    max: 100,
  },
  {
    id: 'power',
    span: 1,
    component: 'input',
    label: 'Power',
    subLabel: 'Fill in a number. (this will get formatted as a number in the formData)',
    parseInput: (val) => Number(val),
    type: 'number',
  },
  {
    id: 'roleModel',
    span: 1,
    component: 'select',
    label: 'Role model',
    subLabel: 'Who do you look up to?',
    slot: [
      {component: 'option', value: '', slot: 'Select one', disabled: true},
      {component: 'option', value: 'captain-america', slot: 'Steve Rogers/Captain America'},
      {component: 'option', value: 'iron-man', slot: 'Tony Stark/Iron Man'},
      {component: 'option', value: 'thor-odinson', slot: 'Thor Odinson'},
      {component: 'option', value: 'the-hulk', slot: 'Bruce Banner/The Hulk'},
      {component: 'option', value: 'black-widow', slot: 'Natasha Romanoff/Black Widow'},
      {component: 'option', value: 'hawkeye', slot: 'Clint Barton/Hawkeye'},
      {component: 'option', value: 'quicksilver', slot: 'Pietro Maximoff/Quicksilver'},
      {component: 'option', value: 'scarlet-witch', slot: 'Wanda Maximoff/Scarlet Witch'},
      {component: 'option', value: 'the-vision', slot: 'The Vision'},
      {component: 'option', value: 'war-machine', slot: 'James Rhodes/War Machine'},
      {component: 'option', value: 'falcon', slot: 'Sam Wilson/Falcon'},
      {component: 'option', value: 'the-winter-soldier', slot: 'Bucky Barnes/The Winter Soldier'},
      {component: 'option', value: 'black-panther', slot: "T'Challa/Black Panther"},
      {component: 'option', value: 'doctor-strange', slot: 'Stephen Strange/Doctor Strange'},
      {component: 'option', value: 'spider-man', slot: 'Peter Parker/Spider-Man'},
      {component: 'option', value: 'ant-man', slot: 'Scott Lang/Ant-Man (Giant-Man)'},
      {component: 'option', value: 'wasp', slot: 'Hope van Dyne/Wasp'},
      {component: 'option', value: 'captain-marvel', slot: 'Carol Danvers/Captain Marvel'},
      {component: 'option', value: 'star-lord', slot: 'Peter Quill/Star-Lord'},
      {component: 'option', value: 'gamora', slot: 'Gamora'},
      {component: 'option', value: 'drax-the-destroyer', slot: 'Drax the Destroyer'},
      {component: 'option', value: 'rocket-raccoon', slot: 'Rocket (Raccoon)'},
      {component: 'option', value: 'groot', slot: '(Baby, Teenage) Groot'},
      {component: 'option', value: 'mantis', slot: 'Mantis'},
      {component: 'option', value: 'daredevil', slot: 'Matthew Murdock/Daredevil'},
      {component: 'option', value: 'jessica-jones', slot: 'Jessica Jones (Jewel)'},
      {component: 'option', value: 'luke-cage', slot: 'Carl Lucas/Luke Cage (Power Man)'},
      {component: 'option', value: 'iron-fist', slot: 'Danny Rand/Iron Fist'},
      {component: 'option', value: 'the-punisher', slot: 'Frank Castle/The Punisher'},
    ],
  },
  {
    id: 'powerUps',
    span: 1,
    // See more info in the Use Custom Components chapter
    component: 'BlitzForm',
    label: 'Choose some power-ups',
    columnCount: 3,
    schema: [
      {
        id: 'iso-8',
        component: 'input',
        type: 'checkbox',
        label: 'Magic crystal',
        labelStyle: 'font-size: 0.8em',
      },
      {
        id: 'hp-potion',
        component: 'input',
        type: 'checkbox',
        label: 'Health potion',
        labelStyle: 'font-size: 0.8em',
      },
      {
        id: 'energy-potion',
        component: 'input',
        type: 'checkbox',
        label: 'Energy drink',
        labelStyle: 'font-size: 0.8em',
      },
    ],
  },
  {span: 1},
  {
    id: 'consent',
    component: 'input',
    type: 'checkbox',
    span: 1,
    label: 'Do you agree with our terms?',
    rules: [(val) => val || 'You must accept our terms'],
    defaultValue: false,
  },
  {
    id: 'submissionDate',
    span: 1,
    component: 'input',
    type: 'date',
    label: 'Date of submission',
  },
]

// eslint-disable-next-line no-unused-vars
const makejson = (json) => {
  let jsonParse = JSON.parse(json)
  let objectProperties = jsonParse.properties;
  // eslint-disable-next-line no-unused-vars
  let nodeList =  Object.keys(objectProperties);
  let itemList = nodeList.map(item =>{
    let temp= {};
    temp = {...objectProperties[item]};
    temp.key = item;
    return temp;
  } )
  let final = itemList.map(item => {
    let output = {}
    output.id = item.key;
    output.span = 1;
    output.label = item.title;

      if (item.type == "integer" || item.type == "string") {
        output.component =  "input";
        output.type = 'text';
      } else if (item.type == 'boolean') {
        output.component =  "input";
        output.type = 'checkbox';
      }else if (item.type == 'array' ){
        output.component =  "select";
        let opt = {};
        opt.component = 'option' ;
        opt.value = '';
        opt.slot=item.items.examples[0];
        output.slot = [];
        output.slot.push( opt)
      }
      return output ;
  })
  return final;

}
const dataModelTest = `{
  "downloadURL": "itms-services://?action=download-manifest&url=https://taraapp.s3.ir-thr-at1.arvanstorage.com/club.plist",
  "buildNumber": 152,
  "versionName": "1.18.2",
  "type": "optional",
  "changeLog": [
    "-رونمایی از تارالند!",
    "- بازطراحی بخش پذیرندگان",
    "- بازطراحی بخش أقساط خُرد تارا",
    "- بهبود برخی از موارد",
    "مادر تلاشیم با ایجادراه‌کارهای جدید و بهبود تارا،رضایت بیشترتون رو جلب کنیم.همین حالا نسخه جدید رو بروز رسانی کن!"
  ]
}`

const formData = ref(JSON.parse(dataModelTest))

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
