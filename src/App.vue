<template>
  <main class="container">
    <Sidebar>
      <ToggleSwitch @switch-toggled="toggleEditMode" label="Edit mode" />
      <div class="sidebar-section">
        <div class="sidebar-title">Left column</div>
        <ColorInput
          label="Highlight color"
          :default-color="colors.left.highlight"
          @color-changed="colors.left.highlight = $event"
        />
        <ColorInput
          label="Background color"
          :default-color="colors.left.background"
          @color-changed="colors.left.background = $event"
        />
        <ColorInput
          label="Text color"
          :default-color="colors.left.text"
          @color-changed="colors.left.text = $event"
        />
      </div>
      <div class="sidebar-section">
        <div class="sidebar-title">Right column</div>
        <ColorInput
          label="Highlight color"
          :default-color="colors.right.highlight"
          @color-changed="colors.right.highlight = $event"
        />
        <ColorInput
          label="Background color"
          :default-color="colors.right.background"
          @color-changed="colors.right.background = $event"
        />
        <ColorInput
          label="Text color"
          :default-color="colors.right.text"
          @color-changed="colors.right.text = $event"
        />
      </div>
      <div class="sidebar-section">
        <PercentageInput
          label="Width of left column"
          :min="20"
          :max="80"
          :current-value="widthLeft"
          @percentage-changed="widthLeft = $event"
        />

        <SelectInput
          label="Headline thickness"
          @update-selection="headlineWeight = $event"
          :default-option="headlineWeight"
          :options="[
            { name: 'Thin', value: '300' },
            { name: 'Medium', value: '400' },
            { name: 'Thick', value: '600' },
          ]"
        />
      </div>

      <div class="sidebar-section">
        <ToggleSwitch @switch-toggled="toggleImageDisplay" label="Show photo" />

        <SelectInput
          label="Photo shape"
          @update-selection="imageShape = $event"
          :default-option="imageShape"
          headlineWeight
          :options="[
            { name: 'Square', value: 'square' },
            { name: 'Round', value: 'round' },
          ]"
        />

        <ImageUpload @image-changed="imageUrl = $event" />
      </div>
    </Sidebar>
    <div
      id="resume"
      class="d-flex"
      :class="{ 'edit-off': !editing }"
      :style="cssVariables"
    >
      <div class="left-col" :style="{ width: percentageWidthLeft }">
        <ResumeSection>
          <img
            v-if="showImage"
            :src="imageUrl"
            alt="profile-pic"
            class="profile-pic"
            :class="{ circle: imageShape == 'round' }"
          />
          <SectionHeadline
            :headline="headlines[0]"
            @headline-edited="updateHeadline($event, 0)"
            :editing="editing"
          />
          <div
            :contenteditable="editing"
            @input="updateProperty($event, 'summary')"
          >
            {{ summary }}
          </div>
        </ResumeSection>
        <ResumeSection>
          <SectionHeadline
            :headline="headlines[1]"
            @headline-edited="updateHeadline($event, 1)"
            :editing="editing"
          />
          <Contact
            :contact="contact"
            @edit="updateNestedProperty"
            :editing="editing"
            :icon-color="colors.left.highlight"
          />
        </ResumeSection>
        <ResumeSection>
          <SectionHeadline
            :headline="headlines[2]"
            @headline-edited="updateHeadline($event, 2)"
            :editing="editing"
          />
          <ul>
            <li
              v-for="(skill, index) in skills"
              :key="index"
              :contenteditable="editing"
              @input="updateNestedProperty($event, 'skills', index)"
            >
              {{ skill }}
            </li>
            <EditButtons
              @addClick="skills.push('new entry')"
              @removeClick="skills.pop()"
              :showRemoveBtn="skills.length > 0"
            />
          </ul>
        </ResumeSection>
        <ResumeSection>
          <SectionHeadline
            :headline="headlines[3]"
            @headline-edited="updateHeadline($event, 3)"
            :editing="editing"
          />
          <ul>
            <li
              v-for="(certification, index) in certifications"
              :key="index"
              :contenteditable="editing"
              @input="updateNestedProperty($event, 'certifications', index)"
            >
              {{ certification }}
            </li>
            <EditButtons
              @addClick="certifications.push('new entry')"
              @removeClick="certifications.pop()"
              :showRemoveBtn="certifications.length > 0"
            />
          </ul>
        </ResumeSection>
      </div>
      <div class="right-col">
        <div
          class="personal-name"
          :contenteditable="editing"
          @input="updateProperty($event, 'name')"
        >
          {{ name }}
        </div>
        <div
          class="personal-title"
          :contenteditable="editing"
          @input="updateProperty($event, 'title')"
        >
          {{ title }}
        </div>
        <ResumeSection>
          <div class="d-flex">
            <SectionHeadline
              :headline="headlines[4]"
              @headline-edited="updateHeadline($event, 4)"
              :editing="editing"
            />
            <EditButtons
              :showRemoveBtn="experience.length > 0"
              @addClick="addExperience"
              textAdd="Add Experience"
            />
          </div>
          <div
            v-for="(item, index) in experience"
            :key="index"
            class="inner-section"
          >
            <div class="d-flex justify-content-between">
              <div
                :contenteditable="editing"
                @input="updateExperience($event, 'title', index)"
              >
                {{ item.title }}
              </div>
              <EditButtons
                @remove-click="removeExperience(index)"
                :showAddBtn="false"
              />
            </div>
            <div class="d-flex justify-content-between">
              <div>
                <span
                  :contenteditable="editing"
                  @input="updateExperience($event, 'company', index)"
                  >{{ item.company }}</span
                >,
                <span
                  :contenteditable="editing"
                  @input="updateExperience($event, 'location', index)"
                  >{{ item.location }}</span
                >
              </div>
              <div
                :contenteditable="editing"
                @input="updateExperience($event, 'date', index)"
              >
                {{ item.date }}
              </div>
            </div>
            <ul>
              <li
                v-for="(desc, innerIndex) in item.description"
                :key="innerIndex"
                :contenteditable="editing"
                @input="updateExperienceDescription($event, index, innerIndex)"
              >
                {{ desc }}
              </li>
              <EditButtons
                @addClick="item.description.push('new entry')"
                @removeClick="item.description.pop()"
                :showRemoveBtn="item.description.length > 0"
              />
            </ul>
          </div>
        </ResumeSection>
        <ResumeSection>
          <div class="d-flex">
            <SectionHeadline
              :headline="headlines[5]"
              @headline-edited="updateHeadline($event, 5)"
              :editing="editing"
            />
            <EditButtons
              :showRemoveBtn="education.length > 0"
              @addClick="addEducation"
              textAdd="Add Education"
            />
          </div>
          <div
            v-for="(item, index) in education"
            :key="index"
            class="inner-section"
          >
            <div class="d-flex justify-content-between">
              <div
                :contenteditable="editing"
                @input="updateEducation($event, 'title', index)"
              >
                {{ item.title }}
              </div>
              <EditButtons
                @remove-click="removeEducation(index)"
                :showAddBtn="false"
              />
            </div>

            <div class="d-flex justify-content-between">
              <div>
                <span
                  :contenteditable="editing"
                  @input="updateEducation($event, 'university', index)"
                >
                  {{ item.university }} </span
                >,
                <span
                  :contenteditable="editing"
                  @input="updateEducation($event, 'location', index)"
                >
                  {{ item.location }}
                </span>
              </div>

              <div
                :contenteditable="editing"
                @input="updateEducation($event, 'date', index)"
              >
                {{ item.date }}
              </div>
            </div>

            <ul>
              <li
                v-for="(desc, innerIndex) in item.description"
                :key="innerIndex"
                :contenteditable="editing"
                @input="updateEducationDescription($event, index, innerIndex)"
              >
                {{ desc }}
              </li>
              <EditButtons
                @addClick="item.description.push('new entry')"
                @removeClick="item.description.pop()"
                :showRemoveBtn="item.description.length > 0"
              />
            </ul>
          </div>
        </ResumeSection>
      </div>
    </div>
  </main>
</template>

<script>
import ResumeSection from './components/ResumeSection.vue';
import SectionHeadline from './components/SectionHeadline.vue';
import Contact from './components/Contact.vue';
import EditButtons from './components/EditButtons.vue';
import ToggleSwitch from './components/ToggleSwitch.vue';
import Sidebar from './components/Sidebar.vue';
import ColorInput from './components/ColorInput.vue';
import PercentageInput from './components/PercentageInput.vue';
import SelectInput from './components/SelectInput.vue';
import ImageUpload from './components/ImageUpload.vue';

export default {
  components: {
    ResumeSection,
    SectionHeadline,
    Contact,
    EditButtons,
    ToggleSwitch,
    Sidebar,
    ColorInput,
    PercentageInput,
    SelectInput,
    ImageUpload,
  },
  data() {
    return {
      colors: {
        left: {
          highlight: '#82C0CC',
          text: '#ffffff',
          background: '#3943B7',
        },
        right: {
          highlight: '#3943B7',
          text: '#000505',
          background: '#ffffff',
        },
      },
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
      editing: true,
      widthLeft: 30,
      imageShape: 'round',
      headlineWeight: '400',
      showImage: true,
    };
  },
  computed: {
    cssVariables() {
      return {
        '--highlight-color-left': this.colors.left.highlight,
        '--background-color-left': this.colors.left.background,
        '--text-color-left': this.colors.left.text,
        '--highlight-color-right': this.colors.right.highlight,
        '--background-color-right': this.colors.right.background,
        '--text-color-right': this.colors.right.text,
        '--headline-weight': this.headlineWeight,
      };
    },
    percentageWidthLeft() {
      return `${this.widthLeft}%`;
    },
  },
  methods: {
    updateHeadline(newValue, index) {
      this.headlines[index] = newValue;
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
    addExperience() {
      this.experience.unshift({
        title: 'Job Title',
        company: 'Company',
        location: 'Location',
        date: 'date range',
        description: ['description'],
      });
    },
    addEducation() {
      this.education.unshift({
        title: 'Education title',
        university: 'University',
        location: 'Location',
        date: 'date range',
        description: ['Summa cum laude, GPA 3.0'],
      });
    },
    removeExperience(index) {
      this.experience.splice(index, 1);
    },
    removeEducation(index) {
      this.education.splice(index, 1);
    },
    toggleEditMode(isChecked) {
      this.editing = isChecked;
    },
    toggleImageDisplay(isChecked) {
      this.showImage = isChecked;
    },
  },
};
</script>

<style scoped>
#resume {
  box-shadow: rgba(50, 50, 93, 0.25) 0 13px 27px -5px,
    rgba(0, 0, 0, 0.3) 0 8px 16px -8px;
  /* height: 297mm; */
  width: 210mm;
  margin-left: auto;
}

#resume.edit-off {
  height: 297mm;
}

@media (min-width: 1350px) {
  #resume {
    margin-left: 300px;
  }
}

@media (min-width: 1600px) {
  #resume {
    margin-left: auto;
    margin-right: auto;
  }
}

.left-col {
  background-color: var(--background-color-left);
  color: var(--text-color-left);
  border-right: 1px solid var(--highlight-color-left);
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
  margin-block-end: 5px;
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
}

.circle {
  border-radius: 50%;
}

.inner-section {
  margin-bottom: 20px;
}

.justify-content-between {
  justify-content: space-between;
}
</style>
