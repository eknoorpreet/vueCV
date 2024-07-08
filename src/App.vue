<template>
  <main class="container">
    <div id="resume" class="d-flex">
      <div class="left-col">
        <div class="resume-section">
          <h4 class="section-headline">About Me</h4>
          <div>
            From data cleaning to data analysis to machine learning, I am
            passionate about everything data
          </div>
        </div>
        <div class="resume-section">
          <h4 class="section-headline">Contact</h4>
          <ul>
            <li>0123456789</li>
            <li>contact@gmail.com</li>
            <li>Quebec St, V5N 2C7, Vancouver, BC, Canada</li>
          </ul>
        </div>
        <div class="resume-section">
          <h4 class="section-headline">Skills</h4>
          <ul>
            <li>Vue</li>
            <li>Java</li>
            <li>PHP</li>
            <li>Python</li>
            <li>TailwindCSS</li>
          </ul>
        </div>
        <div class="resume-section">
          <h4 class="section-headline">Certifications</h4>
          <ul>
            <li>AWS Cloud Practioner (Amazon Web Services)</li>
          </ul>
        </div>
      </div>
      <div class="right-col">
        <div class="personal-name">Eknoorpreet Singh</div>
        <div class="personal-title">Software Engineer (Front-end)</div>
        <div class="resume-section">
          <h4 class="section-headline">Experience</h4>
          <ul>
            <li>
              Developed responsive and interactive web applications using modern
              front-end frameworks such as Vue.js, React, and Angular, improving
              user engagement by 25%.
            </li>
            <li>
              Collaborated with UX/UI designers to implement user-friendly
              interfaces, ensuring cross-browser compatibility and maintaining
              performance optimization across all devices.
            </li>
            <li>
              Integrated RESTful APIs and third-party services to enhance
              functionality and streamline data flow, resulting in a 30%
              reduction in page load times.
            </li>
            <li>
              Utilized version control systems like Git for efficient project
              management and collaborated with back-end developers to ensure
              seamless integration and deployment of web applications.
            </li>
          </ul>
        </div>
        <div class="resume-section">
          <h4 class="section-headline">Education</h4>
          <div>University of British Columbia, Vancouver, BC, 2015 - 2019</div>
          <ul>
            <li>Relevant coursework in algorithms and programming languages</li>
            <li>Project: Recommendation system for Amazon</li>
          </ul>
        </div>
      </div>
    </div>
  </main>
</template>

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
</style>
