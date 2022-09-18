<template>
  <div class="grid grid-cols-6 w-full px-12 mt-16">
    <div
      class="fixed z-50 bottom-8 right-8 rounded-full h-12 w-12 p-8 flex justify-center items-center text-3xl border-blue-500 border-4"
    >
      {{ overall }}
    </div>
    <button
      @click="showSuggestions = !showSuggestions"
      class="fixed top-12 right-8 text-xl text-white rounded-full border border-blue-500 bg-blue-500 px-8 py-4"
      :class="{ hidden: showSuggestions }"
    >
      ← Suggestions
    </button>
    <div
      class="bg-gray-100 rounded-l-lg fixed top-8 right-0 px-8 py-8 max-w-lg z-10"
      :class="{ hidden: !showSuggestions }"
    >
      <h2 class="text-3xl font-bold">Suggestions</h2>
      <p v-if="!badClassifications.length">
        No suggestions available. Excellent job!
      </p>
      <div
        class="mt-4 flex items-center bg-blue-500 text-white text-sm px-4 py-3"
        role="alert"
      >
        <svg
          class="fill-current w-4 h-4 mr-2"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 20 20"
        >
          <path
            d="M12.432 0c1.34 0 2.01.912 2.01 1.957 0 1.305-1.164 2.512-2.679 2.512-1.269 0-2.009-.75-1.974-1.99C9.789 1.436 10.67 0 12.432 0zM8.309 20c-1.058 0-1.833-.652-1.093-3.524l1.214-5.092c.211-.814.246-1.141 0-1.141-.317 0-1.689.562-2.502 1.117l-.528-.88c2.572-2.186 5.531-3.467 6.801-3.467 1.057 0 1.233 1.273.705 3.23l-1.391 5.352c-.246.945-.141 1.271.106 1.271.317 0 1.357-.392 2.379-1.207l.6.814C12.098 19.02 9.365 20 8.309 20z"
          />
        </svg>
        <p>
          <span class="font-bold">Formula:</span> Accomplished X as measured by
          Y, by doing Z.
        </p>
      </div>
      <div
        class="mt-4 bg-blue-100 border-t-4 border-blue-500 rounded-b text-blue-900 px-4 py-3 shadow-md"
        role="alert"
      >
        <div class="flex">
          <div class="py-1">
            <svg
              class="fill-current h-6 w-6 text-blue-500 mr-4"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
            >
              <path
                d="M2.93 17.07A10 10 0 1 1 17.07 2.93 10 10 0 0 1 2.93 17.07zm12.73-1.41A8 8 0 1 0 4.34 4.34a8 8 0 0 0 11.32 11.32zM9 11V9h2v6H9v-4zm0-6h2v2H9V5z"
              />
            </svg>
          </div>
          <div>
            <p class="font-bold">Pssst... here are some general resume tips!</p>
            <ul class="text-sm list-disc">
              <li>
                Make your points as quantifiable as possible! Numbers have
                demonstrate impact effectively.
              </li>
              <li>
                Try to use more action words. They help to create an impression
                when you're delivering information to another reader.
              </li>
              <li>
                Tailor the content of your resume to the job you are applying
                for.
              </li>
            </ul>
          </div>
        </div>
      </div>
      <div
        v-if="badClassifications.length"
        class="mt-4 overflow-y-auto scrollbar-thin scrollbar-track-gray-100 scrollbar-thumb-blue-500 h-64 px-8"
      >
        <div
          class="mt-4"
          v-for="(cls, i) in badClassifications"
          :key="`bad-${i}`"
        >
          <div role="alert">
            <div class="bg-red-500 text-white font-bold rounded-t px-4 py-2">
              {{ cls.input }} (Score: {{ points[cls.input] }})
            </div>
            <div
              class="border border-t-0 border-red-400 rounded-b bg-red-100 px-8 py-3 text-red-700"
            >
              <ul class="list-disc" v-if="points[cls.input] <= 30">
                <li>Add more detail</li>
                <li>Use more action words</li>
              </ul>
              <ul class="list-disc" v-else-if="points[cls.input] <= 75">
                <li>Present your results with quantifiable data</li>
                <li>Demonstrate what you did</li>
              </ul>
              <ul class="list-disc" v-else>
                <li>Emphasize on the impact of your achievement</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
      <button
        @click="showSuggestions = !showSuggestions"
        class="mt-4 text-xl text-white rounded-full border border-blue-500 bg-blue-500 px-8 py-4"
      >
        →
      </button>
    </div>
    <div
      class="col-span-2 flex flex-col overflow-y-scroll h-screen scrollbar-thin scrollbar-track-gray-100 scrollbar-thumb-blue-500 px-4"
    >
      <h3 class="text-2xl">Tell us about yourself</h3>
      <div class="space-y-4 mt-4">
        <label class="block">
          <span class="text-gray-700">Full name</span>
          <input
            type="text"
            class="mt-1 block w-full"
            placeholder="John Doe"
            v-model="informations.name"
          />
        </label>
        <label class="block">
          <span class="text-gray-700">Email</span>
          <input
            type="text"
            class="mt-1 block w-full"
            placeholder="john.doe@email.com"
            v-model="informations.email"
          />
        </label>
        <label class="block">
          <span class="text-gray-700">Phone number</span>
          <input
            type="text"
            class="mt-1 block w-full"
            placeholder="(123) 456-7890"
            v-model="informations.number"
          />
        </label>
        <label class="block">
          <span class="text-gray-700">Location</span>
          <input
            type="text"
            class="mt-1 block w-full"
            placeholder="Waterloo, ON"
            v-model="informations.location"
          />
        </label>
        <label class="block">
          <span class="text-gray-700">Link</span>
          <input
            type="text"
            class="mt-1 block w-full"
            placeholder="mywebsite.com"
            v-model="informations.link"
          />
        </label>
      </div>
      <div class="mt-8" v-for="(edu, i) in educations" :key="`edu-${i}`">
        <hr class="border-t-2 border-blue-500" v-if="i > 0" />
        <h3 class="text-2xl" v-if="i == 0">Education</h3>
        <div class="space-y-4 mt-4">
          <label class="block">
            <span class="text-gray-700">School Name</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="ABC University"
              v-model="edu.school"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">School Location</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Waterloo, ON"
              v-model="edu.location"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">Major</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Computer Science"
              v-model="edu.major"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">GPA</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="4.0"
              v-model="edu.gpa"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">Start Date</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Sep 2020"
              v-model="edu.startDate"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">End Date</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Jun 2024"
              v-model="edu.endDate"
            />
          </label>
        </div>
      </div>
      <button
        class="bg-blue-500 px-8 py-4 text-xl mt-8 font-semibold text-white w-full"
        @click="newEdu"
      >
        Add School
      </button>
      <div class="mt-8" v-for="(exp, i) in experiences" :key="`exp-${i}`">
        <hr class="border-t-2 border-blue-500" v-if="i > 0" />
        <h3 class="text-2xl" v-if="i == 0">Experience</h3>
        <div class="space-y-4 mt-4">
          <label class="block">
            <span class="text-gray-700">Company Name</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Googoool Labz"
              v-model="exp.company"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">Job Title</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Software Engineer"
              v-model="exp.title"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">Job Location</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Mountainview, CA"
              v-model="exp.location"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">Job Responsibilities</span>
            <div
              class="flex gap-4 mb-2"
              v-for="(resp, j) in exp.responsibilities"
              :key="`exp-${i}-resp-${j}`"
            >
              <input
                type="text"
                class="mt-1 block w-full"
                placeholder="Did some stuff"
                v-model="exp.responsibilities[j]"
                @keyup="
                  (event) => {
                    classifyPoint(event, exp.responsibilities[j], i, j)
                  }
                "
              />
              <button
                v-if="j == exp.responsibilities.length - 1"
                class="bg-blue-500 text-white px-4"
                @click="exp.responsibilities.push('')"
              >
                +
              </button>
            </div>
          </label>
          <label class="block">
            <span class="text-gray-700">Start Date</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Apr 2022"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">End Date</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Dec 2022"
            />
          </label>
        </div>
      </div>
      <button
        class="bg-blue-500 px-8 py-4 text-xl mt-8 font-semibold text-white w-full"
        @click="newExp"
      >
        Add Experience
      </button>
      <div class="mt-8" v-for="(skill, i) in skills" :key="`skill-${i}`">
        <hr class="border-t-2 border-blue-500" v-if="i > 0" />
        <h3 class="text-2xl" v-if="i == 0">Skills</h3>
        <div class="space-y-4 mt-4">
          <label class="block">
            <span class="text-gray-700">Skill Name</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Programming"
              v-model="skill.name"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">Skill Details</span>
            <div
              class="flex gap-4 mb-2"
              v-for="(detail, j) in skill.details"
              :key="`skill-${i}-detail-${j}`"
            >
              <input
                type="text"
                class="mt-1 block w-full"
                placeholder="Python"
                v-model="skill.details[j]"
              />
              <button
                v-if="j == skill.details.length - 1"
                class="bg-blue-500 text-white px-4"
                @click="skill.details.push('')"
              >
                +
              </button>
            </div>
          </label>
        </div>
      </div>
      <button
        class="bg-blue-500 px-8 py-4 text-xl mt-8 font-semibold text-white w-full"
        @click="newSkill"
      >
        Add Skill
      </button>
      <div class="mt-8" v-for="(proj, i) in projects" :key="`proj-${i}`">
        <hr class="border-t-2 border-blue-500" v-if="i > 0" />
        <h3 class="text-2xl" v-if="i == 0">Projects</h3>
        <div class="space-y-4 mt-4">
          <label class="block">
            <span class="text-gray-700">Project Name</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Unicorn Startup"
              v-model="proj.name"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">Project Description</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Cures cancer using AI"
              v-model="proj.description"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">Link to Project</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="cancer.ai"
              v-model="proj.link"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">Tools Used</span>
            <div
              class="flex gap-4 mb-2"
              v-for="(tool, j) in proj.tools"
              :key="`proj-${i}-tool-${j}`"
            >
              <input
                type="text"
                class="mt-1 block w-full"
                placeholder="Keras"
                v-model="proj.tools[j]"
              />
              <button
                v-if="j == proj.tools.length - 1"
                class="bg-blue-500 text-white px-4"
                @click="proj.tools.push('')"
              >
                +
              </button>
            </div>
          </label>
        </div>
      </div>
      <button
        class="bg-blue-500 px-8 py-4 text-xl mt-8 font-semibold text-white w-full"
        @click="newProj"
      >
        Add Project
      </button>
      <div class="mt-8" v-for="(award, i) in awards" :key="`award-${i}`">
        <hr class="border-t-2 border-blue-500" v-if="i > 0" />
        <h3 class="text-2xl" v-if="i == 0">Award</h3>
        <div class="space-y-4 mt-4">
          <label class="block">
            <span class="text-gray-700">Award Name</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Nobel Prize"
              v-model="award.name"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">Award Date</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Jan  2024"
              v-model="award.date"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">Awarder</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Nobel Foundation"
              v-model="award.awarder"
            />
          </label>
          <label class="block">
            <span class="text-gray-700">Summary</span>
            <input
              type="text"
              class="mt-1 block w-full"
              placeholder="Implemented world peace using blockchain technology"
              v-model="award.summary"
            />
          </label>
        </div>
      </div>
      <button
        class="bg-blue-500 px-8 py-4 text-xl mt-8 font-semibold text-white w-full"
        @click="newAward"
      >
        Add Award
      </button>
    </div>
    <div class="col-span-4">
      <client-only>
        <vue-html2pdf
          :show-layout="false"
          :float-layout="true"
          :enable-download="true"
          :preview-modal="true"
          :paginate-elements-by-height="1400"
          filename="resume"
          :pdf-quality="2"
          :manual-pagination="false"
          pdf-format="a4"
          :pdf-margin="10"
          pdf-orientation="portrait"
          pdf-content-width="800px"
          ref="html2Pdf"
        >
          <section slot="pdf-content">
            <BuilderTemplateOne
              v-if="template == 0"
              :data="{
                informations,
                educations,
                experiences,
                skills,
                projects,
                awards,
              }"
            />
            <BuilderTemplateTwo
              v-else-if="template == 1"
              :data="{
                informations,
                educations,
                experiences,
                skills,
                projects,
                awards,
              }"
            />
            <BuilderTemplateThree
              v-else-if="template == 2"
              :data="{
                informations,
                educations,
                experiences,
                skills,
                projects,
                awards,
              }"
            />
            <BuilderTemplateFour
              v-else-if="template == 3"
              :data="{
                informations,
                educations,
                experiences,
                skills,
                projects,
                awards,
              }"
            />
          </section>
        </vue-html2pdf>
      </client-only>
      <div class="px-32">
        <BuilderTemplateOne
          v-if="template == 0"
          :data="{
            informations,
            educations,
            experiences,
            skills,
            projects,
            awards,
          }"
        />
        <BuilderTemplateTwo
          v-else-if="template == 1"
          :data="{
            informations,
            educations,
            experiences,
            skills,
            projects,
            awards,
          }"
        />
        <BuilderTemplateThree
          v-else-if="template == 2"
          :data="{
            informations,
            educations,
            experiences,
            skills,
            projects,
            awards,
          }"
        />
        <BuilderTemplateFour
          v-else-if="template == 3"
          :data="{
            informations,
            educations,
            experiences,
            skills,
            projects,
            awards,
          }"
        />
      </div>
    </div>
  </div>
</template>

<script>
const debounce = require('lodash.debounce')
export default {
  name: 'BuilderCreate',
  props: {
    template: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      overall: 0,
      showSuggestions: false,
      informations: [
        {
          name: '',
          email: '',
          number: '',
          link: '',
          location: '',
        },
      ],
      educations: [
        {
          school: '',
          location: '',
          major: '',
          gpa: '',
          startDate: '',
          endDate: '',
        },
      ],
      experiences: [
        {
          company: '',
          title: '',
          location: '',
          responsibilities: [''],
          classifications: {},
          startDate: '',
          endDate: '',
        },
      ],
      skills: [
        {
          name: '',
          details: [''],
        },
      ],
      projects: [
        {
          name: '',
          description: '',
          link: '',
          tools: [''],
        },
      ],
      awards: [
        {
          name: '',
          date: '',
          awarder: '',
          summary: '',
        },
      ],
      points: {},
    }
  },
  methods: {
    newEdu() {
      this.educations.push({
        school: '',
        location: '',
        major: '',
        gpa: '',
        startDate: '',
        endDate: '',
      })
    },
    newExp() {
      this.experiences.push({
        company: '',
        title: '',
        location: '',
        responsibilities: [''],
        classifications: {},
        startDate: '',
        endDate: '',
      })
    },
    newSkill() {
      this.skills.push({
        name: '',
        details: [''],
      })
    },
    newProj() {
      this.projects.push({
        name: '',
        description: '',
        link: '',
        tools: [''],
      })
    },
    newAward() {
      this.awards.push({
        name: '',
        date: '',
        awarder: '',
        summary: '',
      })
    },
    generatePDF() {
      this.$refs.html2Pdf.generatePdf()
    },
    classifyPoint: debounce(async function (event, point, i, j) {
      if (!point) return
      const response = await this.$axios.post(
        'https://api.cohere.ai/classify',
        {
          model: 'large',
          inputs: [point],
          examples: [
            {
              text: 'Developed suggestions engine for store',
              label: 'Bad',
            },
            {
              text: 'Used Google Cloud Recommendations Engine to build a suggestions system for over 10M monthly users of store, boosting sales by 34%',
              label: 'Good',
            },
            {
              text: 'Worked on backend services',
              label: 'Bad',
            },
            {
              text: 'Developed RESTful API using Flask to reduce fetching time by 70%',
              label: 'Good',
            },
            {
              text: 'Updated website design as needed',
              label: 'Bad',
            },
            {
              text: 'Trained employees on using internal tools',
              label: 'Bad',
            },
            {
              text: 'Used Github for collaboration',
              label: 'Bad',
            },
            {
              text: 'Developed mobile application for school, used by over 90% of the population to access important announcements',
              label: 'Good',
            },
            {
              text: 'Created a transaction system with Stripe, boosting sales by 14% and raising overall customer convenience',
              label: 'Good',
            },
            {
              text: 'Implemented machine learning algorithms to detect and remove spam comments with 99% accuracy',
              label: 'Good',
            },
            {
              text: 'Responsible for receiving calls from customers',
              label: 'Bad',
            },
            {
              text: 'Built a chatbot to respond to customer inquiries, increasing 5 star reviews by over 43%',
              label: 'Good',
            },
            {
              text: 'Designed an acronym translator for customer service representatives, facilitating improved responses and increasing overall customer satisfaction',
              label: 'Good',
            },
            {
              text: 'Responded to emails quick',
              label: 'Bad',
            },
            {
              text: 'Created a QR code system for users to use',
              label: 'Bad',
            },
            {
              text: 'Analyzed over $45M of transactions to find patterns in consumer spending, to align marketing efforts towards customer interest',
              label: 'Good',
            },
          ],
        },
        {
          headers: {
            Authorization: 'BEARER IpjO25iPMrxIq5nuSiBOqju8eWTJ06X5KDibjCk6',
            'Content-Type': 'application/json',
          },
        }
      )
      this.$set(
        this.experiences[i].classifications,
        j,
        response.data.classifications
      )
      event.target.classList.add('focus:border-none')
      if (response.data.classifications[0].prediction === 'Good') {
        event.target.classList.add('border-green-500')
        event.target.classList.add('focus:outline-green-500')
        event.target.classList.remove('border-red-500')
        event.target.classList.remove('focus:outline-red-500')
      } else {
        event.target.classList.add('border-red-500')
        event.target.classList.add('focus:outline-red-500')
        event.target.classList.remove('border-green-500')
        event.target.classList.remove('focus:outline-green-500')
      }
    }, 1500),
    async ratePoint(point) {
      const response = await this.$axios.post(
        'https://api.cohere.ai/generate',
        {
          model: 'xlarge',
          prompt: `Rate the following resume points out of 100:\n\nDeveloped QR codes for store\nScore: 30\n\nDeveloped a chatbot to improve customer representative efficiency by 300%\nScore: 95\n\nCreated an API\nScore: 20\n\nDesigned and implemented a real-time marketing campaign\nScore: 90\n\nBuilt a social network for a clothing brand\nScore: 70\n\nImproved site search by 20%\nScore: 60\n\nSaved an e-commerce company $250,000 by reducing a server from four to two\nScore: 90\n\nImplemented machine learning algorithms to detect and remove spam comments with 99% accuracy\nScore: 100\n\nCreated a transaction system with Stripe, boosting sales by 14% and raising overall customer convenience\nScore: 100\n\nUsed Github for collaboration\nScore: 30\n\nTrained employees on using internal tools\nScore: 65\n\nUpdated website design as needed\nScore: 50\n\nDeveloped RESTful API using Flask to reduce fetching time by 70%\nScore: 90\n\nWorked on backend services\nScore: 30\n\nUsed Google Cloud Recommendations Engine to build a suggestions system for over 10M monthly users of store, boosting sales by 34%\nScore: 100\n\nDeveloped suggestions engine for store\nScore: 20\n\n${point}\nScore:`,
          max_tokens: 1,
          temperature: 0.9,
          k: 0,
          p: 0.75,
          frequency_penalty: 0,
          presence_penalty: 0,
          stop_sequences: [],
          return_likelihoods: 'NONE',
        },
        {
          headers: {
            Authorization: 'BEARER IpjO25iPMrxIq5nuSiBOqju8eWTJ06X5KDibjCk6',
            'Content-Type': 'application/json',
            'Cohere-Version': '2021-11-08',
          },
        }
      )
      const score = +response.data.generations[0].text.trim()
      if (isNaN(score)) {
        return await this.ratePoint(point) // try again
      } else {
        this.points[point] = score
        return score
      }
    },
    async overallScore() {
      const scores = await Promise.all(
        this.classifications.map((classification) =>
          this.points[classification.input]
            ? this.points[classification.input]
            : this.ratePoint(classification.input)
        )
      )
      const overall = scores.sort((a, b) => a - b)[
        Math.floor(scores.length / 2)
      ]
      return overall
    },
  },
  computed: {
    classifications() {
      const classifications = []
      for (const experience of this.experiences) {
        for (const classification of Object.values(
          experience.classifications
        )) {
          classifications.push(classification[0])
        }
      }
      return classifications
    },
    goodClassifications() {
      return this.classifications.filter(
        (classification) => classification.prediction === 'Good'
      )
    },
    badClassifications() {
      return this.classifications.filter(
        (classification) => classification.prediction === 'Bad'
      )
    },
  },
  watch: {
    classifications: {
      deep: true,
      handler: function (newVal, oldVal) {
        this.overallScore().then((score) => {
          this.overall = score
        })
      },
    },
  },
}
</script>
