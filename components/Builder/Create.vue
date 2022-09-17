<template>
  <div class="grid grid-cols-6 w-full px-12 mt-16">
    <div
      class="col-span-2 flex flex-col overflow-y-scroll h-screen scrollbar-thin scrollbar-track-gray-100 scrollbar-thumb-red-500 px-4"
    >
      <h3 class="text-2xl">Tell us about yourself</h3>
      <div class="space-y-4 mt-4">
        <label class="block">
          <span class="text-gray-700">Full name</span>
          <input type="text" class="mt-1 block w-full" placeholder="John Doe" />
        </label>
        <label class="block">
          <span class="text-gray-700">Email</span>
          <input
            type="text"
            class="mt-1 block w-full"
            placeholder="john.doe@email.com"
          />
        </label>
        <label class="block">
          <span class="text-gray-700">Phone number</span>
          <input
            type="text"
            class="mt-1 block w-full"
            placeholder="(123) 456-7890"
          />
        </label>
        <label class="block">
          <span class="text-gray-700">Location</span>
          <input
            type="text"
            class="mt-1 block w-full"
            placeholder="Waterloo, ON"
          />
        </label>
        <label class="block">
          <span class="text-gray-700">Link</span>
          <input
            type="text"
            class="mt-1 block w-full"
            placeholder="mywebsite.com"
          />
        </label>
      </div>
      <div class="mt-8" v-for="(edu, i) in educations" :key="`edu-${i}`">
        <hr class="border-t-2 border-red-500" v-if="i > 0" />
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
        class="bg-red-500 px-8 py-4 text-xl mt-8 font-semibold text-white w-full"
        @click="newEdu"
      >
        Add School
      </button>
      <div class="mt-8" v-for="(exp, i) in experiences" :key="`exp-${i}`">
        <hr class="border-t-2 border-red-500" v-if="i > 0" />
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
              />
              <button
                v-if="j == exp.responsibilities.length - 1"
                class="bg-red-500 text-white px-4"
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
        class="bg-red-500 px-8 py-4 text-xl mt-8 font-semibold text-white w-full"
        @click="newExp"
      >
        Add Experience
      </button>
      <div class="mt-8" v-for="(skill, i) in skills" :key="`skill-${i}`">
        <hr class="border-t-2 border-red-500" v-if="i > 0" />
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
                class="bg-red-500 text-white px-4"
                @click="skill.details.push('')"
              >
                +
              </button>
            </div>
          </label>
        </div>
      </div>
      <button
        class="bg-red-500 px-8 py-4 text-xl mt-8 font-semibold text-white w-full"
        @click="newSkill"
      >
        Add Skill
      </button>
      <div class="mt-8" v-for="(proj, i) in projects" :key="`proj-${i}`">
        <hr class="border-t-2 border-red-500" v-if="i > 0" />
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
                class="bg-red-500 text-white px-4"
                @click="proj.tools.push('')"
              >
                +
              </button>
            </div>
          </label>
        </div>
      </div>
      <button
        class="bg-red-500 px-8 py-4 text-xl mt-8 font-semibold text-white w-full"
        @click="newProj"
      >
        Add Project
      </button>
      <div class="mt-8" v-for="(award, i) in awards" :key="`award-${i}`">
        <hr class="border-t-2 border-red-500" v-if="i > 0" />
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
        class="bg-red-500 px-8 py-4 text-xl mt-8 font-semibold text-white w-full"
        @click="newAward"
      >
        Add Award
      </button>
    </div>
    <div class="col-span-4"></div>
  </div>
</template>

<script>
export default {
  name: 'BuilderCreate',
  data() {
    return {
      educationCount: 1,
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
  },
}
</script>
