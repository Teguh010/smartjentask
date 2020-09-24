<template>
  <div class="container">
    <div class="row-ku row ">
      <div class="side-smart col-3 bg-grey ">
        <div class="row q-gutter-x-md justify-center">
          <h2 class="text-white">Smart</h2>
          <h2 class="text-bold text-white">Jen</h2>
        </div>
        <div style="margin-top: -30px;">
          <hr class="hr-smart" />
        </div>
        <div class="q-pt-md">
          <div class="b q-pa-lg text-white">
            With the latest technology of SmartGen now, you can ‘smartly
            generate’ practice questions online instead of traditional way. Do
            not worry about the quiz being too easy or too difficult because
            each topic is preset with thousands of questions in different ranges
            of difficulty. Simply click on the topic, level and adjust the scale
            of difficulty and you will find practice questions specifically
            targeted at your levels of need. You can also save these questions,
            assign them to students and generate progress reports later.
          </div>
        </div>
        <div>
          <div class="q-px-xl">
            <q-img
              alt="smartjen logo"
              src="~assets/smartReading.png"
              style="image-size: 10px;"
            />
          </div>
        </div>
      </div>
      <div class="main-smart col-9 ">
        <div class="row justify-center" style="width: 100%">
          <div class="form-container">
            <div class=" q-pt-md  q-gutter-md q-pb-md">
              <div v-if="tampil" class="q-gutter-md">
                <q-icon name="fas fa-circle" color="blue" size="10px;" />
                <q-icon name="fas fa-circle" color="grey-4" size="10px;" />
                <q-icon name="fas fa-circle" color="grey-4" size="10px;" />
              </div>
              <div v-else class="q-gutter-md">
                <q-icon name="fas fa-circle" color="grey-4" size="10px;" />
                <q-icon name="fas fa-circle" color="blue" size="10px;" />
                <q-icon name="fas fa-circle" color="grey-4" size="10px;" />
              </div>
              <div v-if="step3" class="q-gutter-md">
                <q-icon name="fas fa-circle" color="grey-4" size="10px;" />
                <q-icon name="fas fa-circle" color="grey-4" size="10px;" />
                <q-icon name="fas fa-circle" color="blue" size="10px;" />
              </div>
            </div>
            <div v-if="tampil" class="bg-grey-3">
              <q-form @submit="clickquestions">
                <div class="col q-pt-lg">
                  <div class="q-pl-md q-pt-md" style="margin-bottom: -10px;">
                    Question Bank
                  </div>
                  <div class="q-pa-md row justify-left">
                    <div class="q-gutter-sm row">
                      <q-radio
                        v-model="questionBank"
                        val="public"
                        label="Public Question"
                      />
                      <!-- <q-checkbox v-model="publicQustion" /> -->
                      <!-- <p class="q-pt-md">Public Question</p> -->
                    </div>
                    <div class="q-gutter-sm row q-pl-xl">
                      <q-radio
                        v-model="questionBank"
                        val="private"
                        label="Private Question"
                      />
                      <p class="q-pt-md">Private Question</p>
                    </div>
                  </div>
                  <hr class="doted" />
                </div>

                <div class="q-pl-md q-pb-sm q-pt-sm">
                  Number Of Question
                </div>

                <div class="row q-px-md ">
                  <div class="col">
                    <q-btn
                      label="1"
                      @click="
                        setActive1();
                        setNumber();
                      "
                      :class="{ active: active == 1 }"
                      class="button-number"
                      outline
                      style="color: grey;"
                    >
                    </q-btn>
                  </div>
                  <div class="col">
                    <q-btn
                      @click="
                        setActive2();
                        setNumber();
                      "
                      :class="{ active: active == 2 }"
                      class="button-number"
                      label="2"
                      outline
                      style="color: grey;"
                    />
                  </div>
                  <div class="col">
                    <q-btn
                      @click="
                        setActive3();
                        setNumber();
                      "
                      :class="{ active: active == 3 }"
                      class="button-number"
                      label="3"
                      outline
                      style="color: grey;"
                    />
                  </div>
                  <div class="col">
                    <q-btn
                      @click="
                        setActive4();
                        setNumber();
                      "
                      :class="{ active: active == 4 }"
                      class="button-number"
                      label="4"
                      outline
                      style="color: grey;"
                    />
                  </div>
                  <div class="col">
                    <q-btn
                      @click="
                        setActive5();
                        setNumber();
                      "
                      :class="{ active: active == 5 }"
                      class="button-number"
                      label="5"
                      outline
                      style="color: blue;"
                    />
                  </div>
                  <div class="col-6">
                    <q-select
                      disable
                      label="custom number (premium)"
                      dropdown-icon="edit"
                      class="bg-grey-6 q-px-md"
                      style="border-radius: 3px; height: 40px;"
                      borderless
                      v-model="questionsId"
                      :options="optionsId"
                    />
                  </div>
                </div>
                <div>
                  <div class="q-pt-md">
                    <hr class="doted" />
                  </div>

                  <div class="row q-px-md q-gutter-sm">
                    <div class="col-4">
                      <div class="q-pb-md q-pt-sm">
                        Topics
                      </div>
                      <q-select
                        class="bg-grey-6 q-px-sm"
                        style="border-radius: 3px; height: 40px;"
                        borderless
                        v-model="topicsOptionsSelected"
                        :options="topicsOptions"
                      />
                    </div>
                    <div class="col-4">
                      <div class="q-pb-md q-pt-sm">
                        Learning Objectives
                      </div>
                      <q-select
                        class="bg-grey-6 q-px-sm"
                        style="border-radius: 3px; height: 40px;"
                        borderless
                        v-model="learningObjectivesOptionsSelected"
                        :options="learningObjectivesOptions"
                      />
                    </div>
                    <div class="col-3">
                      <div class="q-pb-md q-pt-sm">
                        Level & Subject
                      </div>
                      <q-select
                        class="bg-grey-6 q-px-sm"
                        style="border-radius: 3px; height: 40px;"
                        borderless
                        v-model="levelnSubjectOptionsSelected"
                        :options="levelnSubjectOptions"
                      />
                    </div>
                  </div>
                </div>
                <div class="q-pt-md">
                  <hr class="doted" />
                </div>
                <div class="q-pl-md q-pt-md">
                  Question Types
                </div>
                <div class="q-px-sm row justify-left">
                  <div class="q-gutter-sm row">
                    <q-checkbox v-model="questionsTypesMcq" />
                    <p class="q-pt-md">MCQ</p>
                  </div>
                  <div class="q-gutter-sm row q-pl-xl">
                    <q-checkbox v-model="questionsTypesNonMcq" />
                    <p class="q-pt-md">Non-MCQ</p>
                  </div>
                </div>
                <div class="q-pt-md">
                  <hr class="doted" />
                </div>
                <div class="q-pl-md  q-pt-md">
                  Dificullity Level
                </div>
                <div class="q-pa-sm row justify-left">
                  <div class="q-gutter-sm row">
                    <q-checkbox v-model="difficultyLevelOptionsEasy" />
                    <p class="q-pt-md">Easy</p>
                  </div>
                  <div class="q-gutter-sm row ">
                    <q-checkbox v-model="difficultyLevelOptionsNormal" />
                    <p class="q-pt-md">Normal</p>
                  </div>
                  <div class="q-gutter-sm row ">
                    <q-checkbox v-model="difficultyLevelOptionsHard" />
                    <p class="q-pt-md">Hard</p>
                  </div>
                  <div class="q-gutter-sm row ">
                    <q-checkbox v-model="difficultyLevelOptionsGenius" />
                    <p class="q-pt-md">Genius</p>
                  </div>
                </div>
                <!-- <div class="row ">
              <div class="col-4 q-pa-md">
                <q-select
                  outlined
                  v-model="questionsCategory"
                  :options="options"
                  label="Outlined"
                />
              </div>
              <div class="col-4 q-pa-md">
                <q-select
                  outlined
                  v-model="questionsGender"
                  :options="optionsGender"
                  label="Outlined"
                />
              </div>
              <div class="col-4 q-pa-md">
                <q-select
                  outlined
                  v-model="questionsHobby"
                  :options="optionsHobby"
                  label="Outlined"
                />
              </div>
              <div class="col-4 q-pa-md">
                <q-select
                  outlined
                  v-model="questionsId"
                  :options="optionsId"
                  label="Outlined"
                />
              </div>
            </div> -->

                <div class="q-pl-md q-pb-lg">
                  <q-btn label="Submit" type="submit" color="primary" />
                  <q-btn
                    label="Reset"
                    type="reset"
                    color="primary"
                    flat
                    class="q-ml-sm"
                  />
                </div>
              </q-form>
            </div>
            <div v-else>
              <!-- <div v-for="question in questions" :key="question.id">
            <div class="bg-red">
              <h4>{{ question.name }}</h4>
            </div>
          </div> -->

              <!-- <div class="q-pa-md" style="max-width: 550px">
                <transition-group name="list" tag="div" class="index">
                  <q-list
                    v-for="(question, index) in questions"
                    :key="question.id"
                  >
                    <q-item>
                      <q-item-section class="bg-black">
                        <q-item-label>{{ question.nama }}</q-item-label>
                        <q-item-label>{{ index + 1 }}</q-item-label>
                        <q-item-label caption lines="2">{{
                          question.descriptions
                        }}</q-item-label>
                      </q-item-section>

                      <q-item-section side top>
                        <q-select
                          style="width: 100px;"
                          :options="optionsTrain"
                          label="Standard"
                          :value="index + 1"
                          @input="
                            newIndex =>
                              moveArrayItemToNewIndex(index, newIndex - 1)
                          "
                        />
                      </q-item-section>
                    </q-item>

                    <q-separator spaced inset />
                  </q-list>
                </transition-group>
              </div> -->
              <q-card style=" width: 120%;">
                <q-card-actions class="bg-primary" align="between">
                  <div class="">
                    <div class="text-h6 text-white">Generate Question</div>
                  </div>
                  <div class=" q-gutter-sm ">
                    <q-btn
                      flat
                      class="bg-red text-capitalize"
                      dense
                      color="white"
                      label="flag"
                      style="width: 90px;"
                    />
                    <q-btn
                      flat
                       class="bg-blue text-capitalize"
                      dense
                      color="white"
                      label="Mqc"
                      style="width: 90px;"
                    />
                    <q-btn
                      flat
                       class="bg-orange text-capitalize"
                      dense
                      color="white"
                      label="Regenerated"
                      style="width: 90px;"
                    />
                  </div>
                </q-card-actions>
              </q-card>
              <q-scroll-area style="height: 700px; width: 120%;">
              <div >
                 <transition-group name="list" tag="div">
                <q-card v-for="(question, index) in questions" :key="question.id" class="" style=" width: 100%;">
                  <q-card-actions style="background-color:#FFF1BD;" align="between">
                    <div class="">
                      <div
                        class="col "
                        style="border-radius: 20px; height:30px; width: 120px; background:#FED33B"
                      >
                        <q-select
                          input-style="color:white"
                          style="height:38px !important;"
                          behavior="menu"
                          borderless
                          class="q-px-lg"
                          :options="optionsTrain"
                          :value="index + 1"
                          @input="
                            newIndex =>
                              moveArrayItemToNewIndex(index, newIndex - 1)
                          "
                        />
                      </div>
                    </div>

                    <div class=" q-gutter-sm q-pr-md">
                      <div>
                        [Whole Numbers] Addition and Substraction of Whole
                        Numbers
                      </div>
                      <div class="text-right">
                        ( 2 Mark, Normal )
                      </div>
                    </div>
                  </q-card-actions>
                  <q-card-actions align="between">
                    <div class="row">
                    <div class="col q-pa-sm">
                      <q-item-label class="text-black"
                        >{{ question.descriptions }}</q-item-label
                      >
                    </div>
                    <div class="q-pt-sm col" style="margin-right: -30px;">
                      <div class="text-center q-gutter-sm" style="margin-bottom: -90px;">
                        <q-btn
                      flat
                      class="bg-red text-capitalize"
                      dense
                      color="white"
                      label="flag"
                      style="width: 90px;"
                    />
                    <q-btn
                      flat
                       class="bg-blue text-capitalize"
                      dense
                      color="white"
                      label="Mqc"
                      style="width: 90px;"
                    />
                    <q-btn
                      flat
                       class="bg-orange text-capitalize"
                      dense
                      color="white"
                      label="Regenerated"
                      style="width: 90px;"
                    />
                      </div>
                    </div>
                    </div>
                  </q-card-actions>
                </q-card>
                </transition-group>
              </div>
                </q-scroll-area>
              <div class="text-right" style="margin-right: -100px;">
                <q-btn label="back" @click="backClick" color="primary" style="width: 90px" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      step3: false,
      active: null,
      issetActive: '',
      optionsTrain: [],
      model: null,

      dense: false,
      denseOpts: false,
      val: true,
      tampil: true,
      questions: [],
      optionsId: [6, 7, 8, 9],

      levelnSubjectOptions: [
        'All',
        'Primary 1 Math',
        'Primary 1 Science',
        'Secondary 2 Science'
      ],
      questionBank: 'Public',
      topicsOptions: ['All', 'Any Standart'],
      anyTopicsOptions: ['All', 'Any Topics'],
      learningObjectivesOptions: ['All', 'Any Heuristic'],
      questionsTypesMcq: true,
      questionsTypesNonMcq: false,

      difficultyLevelOptionsEasy: true,
      difficultyLevelOptionsNormal: false,
      difficultyLevelOptionsHard: false,
      difficultyLevelOptionsGenius: false,

      questionlist: [
        // warning this is just dummy data
        {
          id: 1,
          levelnSubject: 'Primary 1 Math',
          questionBank: 'Public',
          topics: 'Any Standart',
          anyTopics: 'AnyTopics',
          descriptions:
            'firest index Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.',
          learningObjectives: 'Any Heuristic',
          questionTypesMqc: true,
          difficultyLevelEasy: true
        },

        {
          id: 2,
          levelnSubject: 'Primary 1 Math',
          questionBank: 'Public',
          topics: 'Any Standart',
          anyTopics: 'AnyTopics',
          descriptions:
            'second index Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.',
          learningObjectives: 'Any Heuristic',
          questionTypesMqc: true,
          difficultyLevelEasy: true
        },
        {
          id: 3,
          levelnSubject: 'Primary 1 Math',
          questionBank: 'Public',
          topics: 'Any Standart',
          anyTopics: 'AnyTopics',
          descriptions:
            'third index Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.',
          learningObjectives: 'Any Heuristic',
          questionTypesMqc: true,
          difficultyLevelEasy: true
        },
        {
          id: 4,
          levelnSubject: 'Primary 1 Math',
          questionBank: 'Public',
          topics: 'Any Standart',
          anyTopics: 'AnyTopics',
          descriptions:
            'Forth index Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.',
          learningObjectives: 'Any Heuristic',
          questionTypesMqc: true,
          difficultyLevelEasy: true
        },
        {
          id: 5,
          levelnSubject: 'Primary 1 Math',
          questionBank: 'Public',
          topics: 'Any Standart',
          anyTopics: 'AnyTopics',
          descriptions:
            'FIfth Index Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.',
          learningObjectives: 'Any Heuristic',
          questionTypesMqc: true,
          difficultyLevelEasy: true
        },
        {
          id: 6,
          levelnSubject: 'Primary 1 Math',
          questionBank: 'Public',
          topics: 'Any Standart',
          anyTopics: 'AnyTopics',
          descriptions:
            'Sixth Index Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.',
          learningObjectives: 'Any Heuristic',
          questionTypesMqc: true,
          difficultyLevelEasy: true
        },
        {
          id: 7,
          levelnSubject: 'Primary 1 Math',
          questionBank: 'Public',
          topics: 'Any Standart',
          anyTopics: 'AnyTopics',
          descriptions:
            'Seventh index Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.',
          learningObjectives: 'Any Heuristic',
          questionTypesMqc: true,
          difficultyLevelEasy: true
        }
      ],

      levelnSubjectOptionsSelected: 'All',
      topicsOptionsSelected: 'All',
      learningObjectivesOptionsSelected: 'All',

      questionsId: null
    }
  },
  computed: {
    // warning this is just dummy data
    filteredquestionlist: function () {
      const levelnSubject = this.levelnSubjectOptionsSelected
      const topics = this.topicsOptionsSelected
      const learningObjectives = this.learningObjectivesOptionsSelected

      if (
        levelnSubject === 'All' &&
        topics === 'All' &&
        learningObjectives === 'All'
      ) {
        // save performance, juste return the default array:
        return this.questionlist
      } else {
        return this.questionlist.filter(function (question) {
          // return the array after passimng it through the filter function:
          return (
            (levelnSubject === 'All' ||
              question.levelnSubject === levelnSubject) &&
            (topics === 'All' || question.topics === topics) &&
            (learningObjectives === 'All' ||
              question.learningObjectives === learningObjectives)
          )
        })
      }
    }
  },
  methods: {
    clickquestions () {
      this.questions = this.filteredquestionlist.slice(0, this.questionsId)
      this.tampil = false
      const test = this.filteredquestionlist.slice(0, this.questionsId)
      const tests = test.length
      const hasil = Array.from({ length: tests }, (_, i) => i + 1)
      console.log(hasil)
      this.optionsTrain = hasil
      // this.questionsId = this.active
      // console.log(this.optionsId)
    },
    backClick () {
      this.tampil = true
      this.questions = []
    },
    moveArrayItemToNewIndex (oldIndex, newIndex) {
      console.log(oldIndex, newIndex)
      const arr = [...this.questions]

      // if (newIndex >= arr.length) {
      //     let k = newIndex - arr.length;
      //     while (k--) {
      //         arr.push(undefined);
      //     }
      // }

      // arr.splice(newIndex, 0, arr.splice(oldIndex, 1)[0]);

      const tempquestions = arr[oldIndex]
      arr[oldIndex] = arr[newIndex]
      arr[newIndex] = tempquestions

      this.questions = arr
    },
    setActive1 () {
      this.issetActive = 1
    },
    setActive2 () {
      this.issetActive = 2
    },

    setActive3 () {
      this.issetActive = 3
    },
    setActive4 () {
      this.issetActive = 4
    },
    setActive5 () {
      this.issetActive = 5
    },
    setNumber () {
      this.questionsId = this.issetActive
      this.active = this.questionsId
      console.log('questionsId', this.questionsId)
      if (this.questionsId > 5) {
        this.issetActive = ''
      }
    },

    buttonClickOne () {
      const buttons = this.buttons
      let button
      for (button in buttons) {
        console.log('btn', buttons[button])
      }
      //     this.buttons.forEach(function(button) {

      //     buttonid : this.button.id
      //     console.log(buttonid)
      // });
      // var i;
      // for (i = 0; i < buttons.length; i++) {
      //   text += cars[i] + "<br>";
      // }
      // if (this.buttons.id == 1) {
      //   this.button = 1;
      // } else if (this.buttons.id == 2) {
      //   this.button = 2;
      // }
      // console.log(this.button);
    }
  },
  mounted () {}
}
</script>

<style>
.doted {
  border-top: 2px dashed #000;
  width: 93%;
  margin: auto;
  margin-top: 5%;
  margin-bottom: 5%;
  display: block;
  unicode-bidi: isolate;
  margin-block-start: 0.5em;
  margin-block-end: 0.5em;

  border-width: 2.1px;
}
.hr-smart {
  width: 30%;
  margin: auto;
  margin-top: 5%;
  margin-bottom: 5%;
  display: block;
  unicode-bidi: isolate;
  margin-block-start: 0.5em;
  margin-block-end: 0.5em;

  border-width: 2.1px;
}
button.active {
  background-color:#3F3D56 !important;
  color: white !important;
}
.form-container {
  width: 100%;
  max-width: 600px;
}
.list-enter,
.list-leave-to {
  opacity: 0.2;
}

.list-enter-active,
.list-leave-active {
  transition: opacity 0.5s ease;
}

.list-move {
  transition: transform 0.5s ease-out;
}
div.b {
  line-height: 1.6;
  font-size: 15px;
}

/* header
{
    background: green;
    height: 50px;
} */

.side-smart {
  margin-bottom: -110px;
}

Style Attribute {
    color: white;
}
</style>
