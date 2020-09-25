<template>
  <div>
    <div style="background: #f0fffc">
      <div v-if="tampil" class="sidebar bg-primary">
        <div class="row q-gutter-x-md justify-center q-pt-lg">
          <h2 class="text-white">Smart</h2>
          <h2 class="text-bold text-white">Jen</h2>
        </div>
        <div style="margin-top: 30px">
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
              style="image-size: 10px"
            />
          </div>
        </div>
      </div>
      <div>
        <div>
          <div v-if="tampil" class="content">
            <div class="q-gutter-md q-py-md">
              <q-icon name="fas fa-circle" color="blue" size="10px;" />
              <q-icon name="fas fa-circle" color="grey-4" size="10px;" />
              <q-icon name="fas fa-circle" color="grey-4" size="10px;" />
            </div>
            <div class="form-container">
              <q-form
                @submit="clickquestions"
                class="shadow-3"
                style="background: #f0fffc"
              >
                <div class="col q-pt-lg">
                  <div class="q-pl-md q-pt-md question-bank">Question Bank</div>
                  <div class="row justify-left q-pt-md">
                    <div class="col">
                      <q-radio
                        v-model="questionBank"
                        val="public"
                        label="Public Question"
                      />
                      <!-- <q-checkbox v-model="publicQustion" /> -->
                      <!-- <p class="q-pt-md">Public Question</p> -->
                    </div>
                    <div class="col">
                      <q-radio
                        v-model="questionBank"
                        val="private"
                        label="Private Question"
                      />
                    </div>
                  </div>
                  <hr class="doted" />
                </div>

                <div class="q-pl-sm q-pb-sm q-pt-sm">Number Of Question</div>

                <div class="row q-px-sm">
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
                      style="color: grey"
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
                      style="color: grey"
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
                      style="color: grey"
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
                      style="color: grey"
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
                      style="color: blue"
                    />
                  </div>
                  <div class="col-md-6 col-sm-3">
                    <q-select
                      disable
                      label="custom number (premium)"
                      dropdown-icon="edit"
                      class="bg-grey-6 q-px-md"
                      style="border-radius: 3px; height: 37px"
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
                    <div class="col-xs-12 col-sm-6 col-md-4">
                      <div class="q-pb-md q-pt-sm">Topics</div>
                      <q-select
                        class="bg-grey-6 q-px-sm"
                        style="border-radius: 3px; height: 40px"
                        borderless
                        v-model="topicsOptionsSelected"
                        :options="topicsOptions"
                      />
                    </div>
                    <div class="col-xs-12 col-sm-6 col-md-4">
                      <div class="q-pb-md q-pt-sm">Learning Objectives</div>
                      <q-select
                        class="bg-grey-6 q-px-sm"
                        style="border-radius: 3px; height: 40px"
                        borderless
                        v-model="learningObjectivesOptionsSelected"
                        :options="learningObjectivesOptions"
                      />
                    </div>
                    <div class="col-xs-12 col-sm-6 col-md-4">
                      <div class="q-pb-md q-pt-sm">Level & Subject</div>
                      <q-select
                        class="bg-grey-6 q-px-sm"
                        style="border-radius: 3px; height: 40px"
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
                <div class="q-pl-md q-pt-md">Question Types</div>
                <div class="q-px-sm row justify-left">
                  <div class="q-gutter-sm row">
                    <q-radio
                      v-model="questionsTypesMcq"
                      val="MCQ"
                      label="MCQ"
                    />
                  </div>
                  <div class="q-gutter-sm row q-pl-xl">
                    <q-radio
                      v-model="questionsTypesMcq"
                      val="Non-MCQ"
                      label="Non-MCQ"
                    />
                  </div>
                </div>
                <div class="q-pt-md">
                  <hr class="doted" />
                </div>
                <div class="q-pl-md q-pt-md">Dificullity Level</div>
                <div class="q-pa-sm row justify-left">
                  <div class="q-gutter-sm row">
                    <q-checkbox v-model="difficultyLevelOptionsEasy" />
                    <p class="q-pt-md">Easy</p>
                  </div>
                  <div class="q-gutter-sm row">
                    <q-checkbox v-model="difficultyLevelOptionsNormal" />
                    <p class="q-pt-md">Normal</p>
                  </div>
                  <div class="q-gutter-sm row">
                    <q-checkbox v-model="difficultyLevelOptionsHard" />
                    <p class="q-pt-md">Hard</p>
                  </div>
                  <div class="q-gutter-sm row">
                    <q-checkbox v-model="difficultyLevelOptionsGenius" />
                    <p class="q-pt-md">Genius</p>
                  </div>
                </div>
                <div class="q-pl-md q-pb-lg q-pt-md">
                  <q-btn label="Submit" @click="scrollToTop" type="submit" color="primary" />
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
          </div>
          <div v-else class="question-container">
            <div>
              <q-dialog v-model="openFlag">
                <Flag v-model="openFlag" />
              </q-dialog>
            </div>
            <q-page-container>
              <q-page>
                <!-- <q-scroll-area style="height: 700px; width: 120%;"> -->
                <div style="padding-top: 100px">
                  <transition-group name="list" tag="div">
                    <q-card
                      v-for="(question, index) in questions"
                      :key="question.id"
                      class="content-question q-my-md"
                    >
                      <q-card-actions
                        style="background-color: #fff1bd"
                        align="between"
                      >
                        <div
                          style="
                            max-width: 100px;
                            border-radius: 20px;
                            height: 30px;
                            width: 120px;
                            background: #fed33b;
                          "
                        >
                          <q-select
                            input-style="color:white;"
                            style="height: 38px !important"
                            behavior="menu"
                            borderless
                            class="q-px-lg"
                            :options="optionsTrain"
                            :value="index + 1"
                            @input="
                              (newIndex) =>
                                moveArrayItemToNewIndex(index, newIndex - 1)
                            "
                          />
                        </div>
                        <div class="text-right q-gutter-sm">
                          <div class="text-red">
                            [Whole Numbers] Addition and Substraction of Whole
                            Numbers
                          </div>
                          <div class="text-right text-red">
                            ( 2 Mark, Normal )
                          </div>
                        </div>
                      </q-card-actions>
                      <q-card-actions align="between">
                        <div class="row">
                          <div class="col q-pa-sm">
                            <q-item-label
                              class="text-question text-black text-body1"
                              >{{ question.descriptions }}</q-item-label
                            >
                          </div>
                          <div class="btn-question q-pt-sm col">
                            <div class="text-right q-gutter-sm">
                              <q-btn
                                flat
                                @click="openFlag = true"
                                class="bg-red text-capitalize"
                                dense
                                color="white"
                                label="flag"
                                style="width: 90px"
                              />
                              <q-btn
                                flat
                                class="text-capitalize"
                                dense
                                color="black"
                                label="Mqc"
                                style="width: 90px; background: #93f0eb"
                              />
                              <q-btn
                                flat
                                @click="regenerated()"
                                class="text-capitalize"
                                dense
                                color="black"
                                label="Regenerated"
                                style="width: 90px; background: #62f883"
                              />
                            </div>
                          </div>
                        </div>
                      </q-card-actions>
                    </q-card>
                  </transition-group>
                </div>
                <!-- </q-scroll-area> -->
                <div class="q-py-lg btn-back text-right">
                  <q-btn
                    label="back"
                    @click="backClick(); scrollToTop()"
                    color="primary"
                    style="width: 90px"
                  />
                </div>
                <q-page-sticky
                  style="position: fixed; z-index: 5"
                  position="top-left"
                  :offset="[0, 0]"
                >
                  <div class="bg-white q-pa-lg" style="width: 100vw"></div>
                </q-page-sticky>
                <q-page-sticky
                  style="position: fixed; z-index: 10"
                  position="top-left"
                  :offset="[0, 4]"
                >
                  <div class="dot-top q-gutter-md q-pb-md">
                    <div class="q-gutter-md">
                      <q-icon
                        name="fas fa-circle"
                        color="grey-4"
                        size="10px;"
                      />
                      <q-icon name="fas fa-circle" color="blue" size="10px;" />
                      <q-icon
                        name="fas fa-circle"
                        color="grey-4"
                        size="10px;"
                      />
                    </div>
                    <div v-if="step3" class="q-gutter-md">
                      <q-icon
                        name="fas fa-circle"
                        color="grey-4"
                        size="10px;"
                      />
                      <q-icon
                        name="fas fa-circle"
                        color="grey-4"
                        size="10px;"
                      />
                      <q-icon name="fas fa-circle" color="blue" size="10px;" />
                    </div>
                  </div>
                </q-page-sticky>
                <q-page-sticky
                  :offset="[6, 45]"
                  expand
                  position="top"
                  style="position: fixed; z-index: 10"
                >
                  <q-card class="header-content">
                    <q-card-actions class="bg-primary" align="between">
                      <div class="">
                        <div class="text-h6 text-white">Generate Question</div>
                      </div>
                      <div class="q-gutter-sm">
                        <q-btn
                          @click="openFlag = true"
                          flat
                          class="bg-red text-capitalize"
                          dense
                          color="black"
                          label="flag"
                          style="width: 90px"
                        />
                        <q-btn
                          flat
                          class="text-capitalize"
                          dense
                          color="black"
                          label="Mqc"
                          style="width: 90px; background: #93f0eb"
                        />
                        <q-btn
                          flat
                          @click="regenerated()"
                          class="text-capitalize"
                          dense
                          color="black"
                          label="Regenerated All"
                          style="width: 120px; background: #62f883"
                        />
                      </div>
                    </q-card-actions>
                  </q-card>
                </q-page-sticky>
              </q-page>
            </q-page-container>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Flag from 'pages/Modal.vue'
export default {
  components: {
    Flag
  },
  data () {
    return {
      openFlag: false,
      question: 'test',
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
      questionsTypesMcq: 'MCQ',

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
            'first index Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.',
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
    },
    regenerated () {
      this.random = Math.floor(Math.random() * 3) + 0

      this.question = this.questionlist[this.random]
      console.log(this.question)
    },
    scrollToTop () {
      window.scrollTo(0, 0)
    }
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400;600&display=swap");
.container {
  font-family: "Open Sans", sans-serif;
  font-weight: 500;
}
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
  background-color: #3f3d56 !important;
  color: white !important;
}
.form-container {
  width: 100%;
  max-width: 800px;
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

.side-smart {
  margin-bottom: 0px;
}
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.sidebar {
  margin: 0;
  padding: 0;
  width: 500px;
  background-color: #f1f1f1;
  position: fixed;
  height: 100%;
  overflow: auto;
}

.content {
  margin-left: 700px;
  padding: 1px 20px;
  height: 1000px;
}
.content-question {
  width: 100%;
}
.header-content {
  width: 100%;
}
.btn-question {
  margin-right: 0px;
}
.question-container {
  padding: 10px 50px 10px 50px;
}
.text-question {
  line-height: 2.6;
}
.dot-top {
  posistion: fixed;
}
@media screen and (max-width: 700px) {
  .sidebar {
    width: 100%;
    height: auto;
    position: relative;
  }
  .header-content {
    width: 100%;
  }
  .content-question {
    width: 100% !important;
  }
  .btn-back {
    margin-right: 10px;
  }
  .sidebar a {
    float: left;
  }
  div.content {
    margin-left: 0;
  }
}
.sub-content-question {
  flex-direction: column-reverse;
  display: flex;
}
.question-bank {
  margin-left: -5px;
}
.question-container {
  padding: 10px 10px 10px 10px;
}

@media screen and (max-width: 400px) {
  .question-container {
    padding: 10px 10px 10px 10px;
  }
}
@media screen and (max-width: 350px) {
  /* .header-content {
    width: 100%;
  }
  .content-question{
    width: 100% !important;
  }
  .sidebar a {
    text-align: center;
    float: none;
  } */
}
</style>
