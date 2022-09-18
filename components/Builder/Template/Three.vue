<template>
  <div class="p-5">
    <h1 class="text-4xl text-center leading-15 underline">
      {{ data.informations.name }}
    </h1>
    <div class="h-full flex justify-around">
      <h3 class="center">{{ data.informations.email }}</h3>
      <h3 class="center">{{ data.informations.number }}</h3>
      <h3 class="center">{{ data.informations.location }}</h3>
      <h3 class="center">{{ data.informations.link }}</h3>
    </div>
    <h2 class="font-bold text-center underline">Education</h2>
    <span
      class="list-disc ml-8"
      v-for="(edu, i) in data.educations"
      :key="`edu-${i}`"
    >
      <span style="list-style-position: inside">
        <b>{{ edu.school }}</b> - {{ edu.major }} - GPA: {{ edu.gpa }}
        <p class="float-right mr-[0%]">
          {{ edu.startDate }} - {{ edu.endDate }}
        </p>
        <br />
        <p class="float-right mr-[0%]">{{ edu.location }}</p>
        <br
      /></span>
    </span>
    <h2 class="font-bold text-center underline">Experience</h2>
    <ul
      class="list-disc ml-8"
      v-for="(exp, i) in data.experiences"
      :key="`exp-${i}`"
    >
      <u>{{ exp.company }}</u>
      <p class="float-right mr-[0%]">{{ exp.startDate }} - {{ exp.endDate }}</p>
      <br />
      <span class="ml-6">{{ exp.title }}</span>
      <p class="float-right margin-right">{{ exp.location }}</p>
      <li
        class="list-disc ml-10"
        v-for="(res, j) in exp.responsibilities"
        :key="`exp-${i}-res-${j}`"
      >
        {{ res }}
      </li>
    </ul>
    <h2 class="font-bold text-center underline">Skills</h2>
    <ul
      class="list-disc ml-8"
      v-for="(skill, i) in data.skills"
      :key="`skill-${i}`"
    >
      <u>{{ skill.name }}</u
      ><br />
      <li
        class="ml-10"
        v-for="(res, j) in skill.details"
        :key="`skill-${i}-res-${j}`"
      >
        {{ res }}
      </li>
    </ul>
    <h2 class="font-bold text-center underline">Projects</h2>
    <span class="ml-8" v-for="(proj, i) in data.projects" :key="`proj-${i}`">
      <u>{{ proj.name }}</u> - {{ proj.tools.join(', ') }} <br />
      <span class="ml-8">{{ proj.link }}</span>
      <li class="ml-12">{{ proj.description }}</li>
    </span>
    <h2 class="font-bold text-center underline">Awards</h2>
    <ul
      class="list-disc ml-8"
      v-for="(award, i) in data.awards"
      :key="`award-${i}`"
    >
      <u>{{ award.name }}</u>
      <p class="float-right mr-[0%]">{{ award.date }}</p>
      <br />
      <span>Awarded By: {{ award.awarder }}</span>
      <li class="ml-8">{{ award.summary }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'BuilderTemplateThree',
  props: {
    data: {
      type: Object,
      default: () => ({}),
    },
  },
}
</script>
