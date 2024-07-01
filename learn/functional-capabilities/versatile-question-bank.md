# Versatile Question Bank

### <mark style="color:orange;">What is a Question Bank?</mark>

Question Bank is a collection of questions that the creator can create for repeated use by users. Users can discover the questions on the learning apps and consume them using the question set player. **Question set player** has the following capabilities:

1. Supports online and offline consumption
2. Embeddable across learning apps

### <mark style="color:orange;">How to Create a Question Bank?</mark>

Questions can be created using the **question set editor,** which has the following capabilities:

1. Multiple question set categories to choose from and organised into different categories such as:
   * **Quiz:** Test the knowledge of participating users using time-bound standalone quizzes and their scores' analysis
   * **Practice Test:** Allows users to practice questions on important topics inside courses
   * **Surveys:** Allows users to take surveys for the creator
   * **Assessments:** Enable assessments inside courses for users to get a good understanding of topics and provide rewards using scores as well
2. Different types of Questions can be utilised for the categories above:
   * **Multiple choice questions**: The Multiple Choice Question (MCQ) allows users to select one or more correct answer(s) from a number of potential answers. There are various layout template options for this question type.
   * **Subjective questions** - Allows users to enter text in response to questions given by the creator.
   * **Fill in the blanks**: Allows users to type their responses into empty response boxes that have been inserted by the creator (To be developed)
   * **Match the following**: Allows users to match questions to the correct responses to pair associated items (To be developed)
   * **Math questions**: Math questions are backed by MathJax, which understands mathematical syntax and rules. Create open-ended math questions that have equations, expressions, etc.
   * **Chemistry Questions**: Powered by LATEX, LATEX is used worldwide for scientific documents, books, and many other forms of publishing.
3. Configurable behaviors
   * **Scoring** - Creators can provide different scores to different questions or can also choose the questions to be auto-scored
   * **Single or Multiple sections** - The Creator can choose to enable sections
   * **Instructions** - Provide users with instructions before the Question set. The Creator can also give instructions before each section as well.
   * **Shuffle questions** - Choose to auto-shuffle questions to each user
   * **Duration** - Set the time for a particular question
   * **Layout** - Choose different layouts for questions to be displayed in
     * Horizontal
     * Vertical
     * Grid
     * 2-Column
     * 3-Column

### <mark style="color:orange;">How can this feature be used?</mark>

#### Use Cases of Question Banks and Telemetry

**Question Banks**

1. **Academic Assessment**: Utilize in academic settings for standardized testing, mid-terms, finals, or entrance exams to gauge student understanding and proficiency.
2. **Corporate Training & Assessment**: Design pre-employment assessments or ongoing skill evaluations for employees to ensure they meet job requirements.
3. **Licensing & Certification**: Use for the administration of professional certification and licensing exams across various professions.
4. **Online Courses and MOOCs**: Embed in Massive Open Online Courses (MOOCs) and e-learning platforms for module quizzes, end-of-course exams, and self-assessment tools.
5. **Survey Research**: Create and distribute surveys for academic research, market research, or customer feedback.

**Telemetry**

1. **Learning Analytics**: Gain insights into how students interact with educational content, identify common misconceptions, and adjust teaching methods accordingly.
2. **User Engagement Analysis**: Measure engagement levels across different modules or platforms to improve user interface and learning experience.
3. **Content Performance**: Analyze which questions or topics are well-understood and which need revisiting or additional resources, guiding content improvement.
4. **Adaptive Learning Pathways**: Utilize data to personalize learning experiences, enabling platforms to suggest more relevant content based on user performance and behavior.
5. **Predictive Analysis**: Use historical data to predict future trends such as exam outcomes or course completion rates, assisting in early intervention strategies.

**Integrated Use Cases**

1. **Targeted Intervention**: Combine question bank results with telemetry data to identify areas where students struggle, allowing for targeted educational interventions.
2. **Skill Gap Analysis**: Employ within companies to determine skill gaps among employees, guiding training programs and personal development plans.
3. **Curriculum Development**: Inform curriculum designers by showing what students have mastered and where gaps persist, leading to informed course adjustments.
4. **Policy Making in Education**: Influence educational policy by providing data-driven insights into student performance at a granular level, facilitating systemic educational improvements.
5. **Feedback Loop for Continuous Improvement**: Create a feedback loop for content creators, educators, and platform developers to continuously improve learning materials and platforms based on actual user data and performance.

Question set player emits **telemetry data** (i.e. signals) for each action performed by the user. This makes a rich data pool available, which can be aggregated to get all types of insights. It is through these insights that various actors can make informed decisions. Data Dashboards are available on the consumption interfaces to show progress at the individual or institutional level.&#x20;

For example, imagine a set of tests held at engineering colleges to help identify the concepts where most students are weak. The aggregated data across geography, made available to the right stakeholders at the right time, helps arrive at timely interventions and long-term plans (like maybe the base of this concept isn’t understood well during high school, and the intervention is to be done then).

### <mark style="color:orange;">How to Configure?</mark>

The above capabilities of Question Bank are derived from components of Sunbird InQuiry. You can find details by clicking on the link below.

{% hint style="info" %}
Further details on [versatile-question-bank.md](product-and-developers-guide/versatile-question-bank.md "mention")
{% endhint %}

**Note**: The complete capabilities of inQuiry still need to be integrated within ED. You'll need to validate the workflows if you use inQuiry BB for your instance.
