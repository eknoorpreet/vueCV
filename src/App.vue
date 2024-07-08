<template>
  <main class="container">
    <div id="resume" class="d-flex">
      <div class="left-col">
        <div class="resume-section">
          <img :src="imageUrl" alt="profile-pic" class="profile-pic" />
          <h4
            class="section-headline"
            contenteditable="true"
            @input="updateHeadline($event, 0)"
          >
            {{ headlines[0] }}
          </h4>
          <div
            contenteditable="true"
            @input="updateProperty($event, 'summary')"
          >
            {{ summary }}
          </div>
        </div>
        <div class="resume-section">
          <h4
            class="section-headline"
            contenteditable="true"
            @input="updateHeadline($event, 1)"
          >
            {{ headlines[1] }}
          </h4>
          <ul>
            <li
              contenteditable="true"
              @input="updateNestedProperty($event, 'contact', 'phone')"
            >
              {{ contact.phone }}
            </li>
            <li
              contenteditable="true"
              @input="updateNestedProperty($event, 'contact', 'email')"
            >
              {{ contact.email }}
            </li>
            <li
              contenteditable="true"
              @input="updateNestedProperty($event, 'contact', 'address')"
            >
              {{ contact.address }}
            </li>
          </ul>
        </div>
        <div class="resume-section">
          <h4
            class="section-headline"
            contenteditable="true"
            @input="updateHeadline($event, 2)"
          >
            {{ headlines[2] }}
          </h4>
          <ul>
            <li
              v-for="(skill, index) in skills"
              :key="index"
              contenteditable="true"
              @input="updateNestedProperty($event, 'skills', index)"
            >
              {{ skill }}
            </li>
          </ul>
        </div>
        <div class="resume-section">
          <h4
            class="section-headline"
            contenteditable="true"
            @input="updateHeadline($event, 3)"
          >
            {{ headlines[3] }}
          </h4>
          <ul>
            <li
              v-for="(certification, index) in certifications"
              :key="index"
              contenteditable="true"
              @input="updateNestedProperty($event, 'certifications', index)"
            >
              {{ certification }}
            </li>
          </ul>
        </div>
      </div>
      <div class="right-col">
        <div
          class="personal-name"
          contenteditable="true"
          @input="updateProperty($event, 'name')"
        >
          {{ name }}
        </div>
        <div
          class="personal-title"
          contenteditable="true"
          @input="updateProperty($event, 'title')"
        >
          {{ title }}
        </div>
        <div class="resume-section">
          <h4
            class="section-headline"
            contenteditable="true"
            @input="updateHeadline($event, 4)"
          >
            {{ headlines[4] }}
          </h4>
          <div
            v-for="(item, index) in experience"
            :key="index"
            class="inner-section"
          >
            <div
              contenteditable="true"
              @input="updateEducation($event, 'title', index)"
            >
              {{ item.title }}
            </div>
            <div class="d-flex justify-content-between">
              <div>
                <span
                  contenteditable="true"
                  @input="updateExperience($event, 'company', index)"
                  >{{ item.company }}</span
                >,
                <span
                  contenteditable="true"
                  @input="updateExperience($event, 'location', index)"
                  >{{ item.location }}</span
                >
              </div>
              <div
                contenteditable="true"
                @input="updateExperience($event, 'date', index)"
              >
                {{ item.date }}
              </div>
            </div>
            <ul>
              <li
                v-for="(desc, innerIndex) in item.description"
                :key="innerIndex"
                contenteditable="true"
                @input="updateExperienceDescription($event, index, innerIndex)"
              >
                {{ desc }}
              </li>
            </ul>
          </div>
        </div>
        <div class="resume-section">
          <h4
            class="section-headline"
            contenteditable="true"
            @input="updateHeadline($event, 5)"
          >
            {{ headlines[5] }}
          </h4>
          <div
            v-for="(item, index) in education"
            :key="index"
            class="inner-section"
          >
            <div
              contenteditable="true"
              @input="updateEducation($event, 'title', index)"
            >
              {{ item.title }}
            </div>

            <div class="d-flex justify-content-between">
              <div>
                <span
                  contenteditable="true"
                  @input="updateEducation($event, 'university', index)"
                >
                  {{ item.university }} </span
                >,
                <span
                  contenteditable="true"
                  @input="updateEducation($event, 'location', index)"
                >
                  {{ item.location }}
                </span>
              </div>

              <div
                contenteditable="true"
                @input="updateEducation($event, 'date', index)"
              >
                {{ item.date }}
              </div>
            </div>

            <ul>
              <li
                v-for="(desc, innerIndex) in item.description"
                :key="innerIndex"
                contenteditable="true"
                @input="updateEducationDescription($event, index, innerIndex)"
              >
                {{ desc }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      name: 'Eknoorpreet Singh',
      title: 'Software Engineer (Front-end)',
      summary:
        'From data cleaning to data analysis to machine learning, I am passionate about everything data',
      imageUrl: '/happy-smiling-young-man.jpg',
      headlines: [
        'About me',
        'Contact',
        'Skills',
        'Certifications',
        'Experience',
        'Education',
      ],
      contact: {
        phone: '0123456789',
        email: 'contact@gmail.com',
        address: 'Quebec St, V5N 2C7, Vancouver, BC, Canada',
      },
      skills: [
        'Java',
        'PHP',
        'Laravel',
        'Node.js',
        'Express',
        'REST',
        'MongoDB',
        'SQL (PostgreSQL, MySQL)',
        'Socket.io',
        'HTML5',
        'CSS3',
        'React.js',
        'JavaScript',
        'SASS',
        'Next.js',
        'TypeScript',
      ],
      experience: [
        {
          title: 'Full-stack Developer',
          company: 'Dropbox',
          location: 'Vancouver, BC',
          date: '2022 - Present',
          description: [
            'Developed responsive and interactive web applications using modern front-end frameworks such as Vue.js and React, improving user engagement by 25%.',
            'Collaborated with UX/UI designers to implement user-friendly interfaces, ensuring cross-browser compatibility',
            'Integrated RESTful APIs and third-party services to enhance functionality, resulting in a 30% reduction in page load times.',
          ],
        },
        {
          title: 'Front-end Developer',
          company: 'Amazon',
          location: 'Vancouver, BC',
          date: '2019 - 2022',
          description: [
            'Utilized version control systems like Git for efficient project management and collaborated with back-end developers.',
            'Led the migration of legacy codebases to modern JavaScript frameworks, reducing technical debt by 40%.',
            'Conducted code reviews and provided mentorship to junior developers, fostering a culture of continuous code quality improvements within the team.',
          ],
        },
        {
          title: 'Software Engineer',
          company: 'New York Times',
          location: 'New York, NY',
          date: '2017 - 2019',
          description: [
            'Conducted code reviews and provided mentorship to junior developers, fostering a culture of continuous learning and code quality improvements within the team.',
            'Implemented automated testing frameworks, increasing test coverage by 50% and significantly reducing the number of bugs in production releases.',
            'Optimized web application performance by analyzing and addressing bottlenecks, resulting in a 20% improvement in load times and overall user experience.',
          ],
        },
      ],
      education: [
        {
          title: 'Master of Science in Computer Science',
          university: 'Georgia Institute of Technology',
          location: 'Atlanta, GA',
          date: '2019-2021',
          description: [
            'Coursework included advanced machine learning, statistical modeling, and data visualization techniques.',
            "Thesis: 'Predictive Modeling for Customer Churn in E-commerce using Random Forest.'",
          ],
        },
        {
          title: 'Bachelor of Science in Computer Science',
          university: 'University of British Columbia',
          location: 'Vancouver, BC',
          date: '2015-2019',
          description: [
            'Relevant coursework in database management, algorithms, and programming languages.',
            "Senior project: 'Development of a Recommender System for Movie Ratings.'",
          ],
        },
      ],
      certifications: [
        'AWS Cloud Practitoner (Amazon Web Services)',
        'Vue JS Essentials with Vuex and Vue Router (Udemy)',
      ],
    };
  },
  methods: {
    updateHeadline(event, index) {
      this.headlines[index] = event.target.innerText;
    },
    updateProperty(event, key) {
      this[key] = event.target.innerText;
    },
    updateNestedProperty(event, key1, key2) {
      this[key1][key2] = event.target.innerText;
    },
    updateExperience(event, key, index) {
      this.experience[index][key] = event.target.innerText;
    },
    updateExperienceDescription(event, index1, index2) {
      this.experience[index1]['description'][index2] = event.target.innerText;
    },
    updateEducation(event, key, index) {
      this.education[index][key] = event.target.innerText;
    },
    updateEducationDescription(event, index1, index2) {
      this.education[index1]['description'][index2] = event.target.innerText;
    },
  },
};
</script>

<style scoped>
#resume {
  box-shadow: rgba(50, 50, 93, 0.25) 0 13px 27px -5px,
    rgba(0, 0, 0, 0.3) 0 8px 16px -8px;
  height: 297mm;
  width: 210mm;
}

.left-col {
  background-color: var(--background-color-left);
  color: var(--text-color-left);
  border-right: 1px solid var(--highlight-color-left);
  width: 30%;
  padding: 30px;
}

.right-col {
  background-color: var(--background-color-right);
  color: var(--text-color-right);
  width: 70%;
  padding: 30px;
}

.section-headline {
  font-size: 20px;
  font-weight: var(--headline-weight);
  margin-bottom: 15px;
  margin-top: 0;
}

.left-col .section-headline {
  border-bottom: 1px solid var(--highlight-color-left);
  padding-bottom: 5px;
  margin-right: -30px;
  padding-right: 10px;
  color: var(--highlight-color-left);
}

.right-col .section-headline {
  color: var(--highlight-color-right);
}

.resume-section {
  margin-bottom: 30px;
}

.personal-name {
  font-weight: 300;
  color: var(--highlight-color-right);
  font-size: 28px;
  border-bottom: 1px solid var(--highlight-color-right);
  margin: 0;
  margin-left: -30px;
  padding-left: 30px;
  padding-bottom: 15px;
}

.personal-title {
  border-bottom: 1px solid var(--highlight-color-right);
  margin: 0 0 20px -30px;
  padding: 15px 0 15px 30px;
  font-weight: 300;
  font-size: 20px;
}

#resume ul {
  padding-inline-start: 16px;
  margin-block-end: 0px;
  margin-block-start: 5px;
}

.profile-pic {
  display: block;
  width: 160px;
  height: 160px;
  border: 5px solid var(--highlight-color-left);
  margin-bottom: 20px;
  object-fit: cover;
  margin-left: auto;
  margin-right: auto;
  border-radius: 50%;
}

.inner-section {
  margin-bottom: 20px;
}

.justify-content-between {
  justify-content: space-between;
}
</style>
