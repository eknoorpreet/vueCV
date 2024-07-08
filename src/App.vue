<template>
  <main class="container">
    <div id="resume" class="d-flex">
      <div class="left-col">
        <div class="resume-section">
          <img :src="imageUrl" alt="profile-pic" class="profile-pic" />
          <h4 class="section-headline">{{ headlines[0] }}</h4>
          <div>
            {{ summary }}
          </div>
        </div>
        <div class="resume-section">
          <h4 class="section-headline">{{ headlines[1] }}</h4>
          <ul>
            <li>{{ contact.phone }}</li>
            <li>{{ contact.email }}</li>
            <li>{{ contact.address }}</li>
          </ul>
        </div>
        <div class="resume-section">
          <h4 class="section-headline">{{ headlines[2] }}</h4>
          <ul>
            <li v-for="(skill, index) in skills" :key="index">{{ skill }}</li>
          </ul>
        </div>
        <div class="resume-section">
          <h4 class="section-headline">{{ headlines[3] }}</h4>
          <ul>
            <li>AWS Cloud Practioner (Amazon Web Services)</li>
          </ul>
        </div>
      </div>
      <div class="right-col">
        <div class="personal-name">Eknoorpreet Singh</div>
        <div class="personal-title">Software Engineer (Front-end)</div>
        <div class="resume-section">
          <h4 class="section-headline">{{ headlines[4] }}</h4>
          <div
            v-for="(item, index) in experience"
            :key="index"
            class="inner-section"
          >
            <div>{{ item.title }}</div>
            <div class="d-flex justify-content-between">
              <div>{{ item.company }}, {{ item.location }}</div>
              <div>{{ item.date }}</div>
            </div>
            <ul>
              <li
                v-for="(desc, innerIndex) in item.description"
                :key="innerIndex"
              >
                {{ desc }}
              </li>
            </ul>
          </div>
        </div>
        <div class="resume-section">
          <h4 class="section-headline">{{ headlines[5] }}</h4>
          <div v-for="(item, index) in education" :key="index">
            <div>{{ item.title }}</div>
            <div class="d-flex justify-content-between">
              <div>{{ item.university }}, {{ item.location }}</div>
              <div>{{ item.date }}</div>
            </div>
            <ul>
              <li
                v-for="(desc, innerIndex) in item.description"
                :key="innerIndex"
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
    };
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
