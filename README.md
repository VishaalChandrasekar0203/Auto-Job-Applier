# Auto-Job-Applier


Installation
Confirmed successful runs on the following:

Operating Systems:
Windows 10
Ubuntu 22
Python versions:
3.10
3.11.9(64b)
3.12.5(64b)
Download and Install Python:

Ensure you have the last Python version installed. If not, download and install it from Python's official website. For detailed instructions, refer to the tutorials:

How to Install Python on Windows
How to Install Python on Linux
How to Download and Install Python on macOS
Download and Install Google Chrome:

Download and install the latest version of Google Chrome in its default location from the official website.
Clone the repository:

git clone https://github.com/feder-cr/Auto_Jobs_Applier_AIHawk.git

cd Auto_Jobs_Applier_AIHawk
Activate virtual environment:

python3 -m venv virtual
source virtual/bin/activate
or for Windows-based machines -

.\virtual\Scripts\activate
Install the required packages:

pip install -r requirements.txt
Configuration
1. secrets.yaml
This file contains sensitive information. Never share or commit this file to version control.

llm_api_key: [Your OpenAI or Ollama API key or Gemini API key]
Replace with your OpenAI API key for GPT integration
To obtain an API key, follow the tutorial at: https://medium.com/@lorenzozar/how-to-get-your-own-openai-api-key-f4d44e60c327
Note: You need to add credit to your OpenAI account to use the API. You can add credit by visiting the OpenAI billing dashboard.
According to the OpenAI community and our users' reports, right after setting up the OpenAI account and purchasing the required credits, users still have a Free account type. This prevents them from having unlimited access to OpenAI models and allows only 200 requests per day. This might cause runtime errors such as:
Error code: 429 - {'error': {'message': 'You exceeded your current quota, please check your plan and billing details. ...}}
{'error': {'message': 'Rate limit reached for gpt-4o-mini in organization <org> on requests per day (RPD): Limit 200, Used 200, Requested 1.}}
OpenAI will update your account automatically, but it might take some time, ranging from a couple of hours to a few days.
You can find more about your organization limits on the official page.
For obtaining Gemini API key visit Google AI for Devs
2. config.yaml
This file defines your job search parameters and bot behavior. Each section contains options that you can customize:

remote: [true/false]

Set to true to include remote jobs, false to exclude them
experienceLevel:

Set desired experience levels to true, others to false
jobTypes:

Set desired job types to true, others to false
date:

Choose one time range for job postings by setting it to true, others to false
positions:

List job titles you're interested in, one per line

Example:

positions:
  - Software Developer
  - Data Scientist
locations:

List locations you want to search in, one per line

Example:

locations:
  - Italy
  - London
apply_once_at_company: [True/False]

Set to True to apply only once per company, False to allow multiple applications per company
distance: [number]

Set the radius for your job search in miles
Example: distance: 50
companyBlacklist:

List companies you want to exclude from your search, one per line

Example:

companyBlacklist:
  - Company X
  - Company Y
titleBlacklist:

List keywords in job titles you want to avoid, one per line

Example:

titleBlacklist:
  - Sales
  - Marketing
2.1 config.yaml - Customize LLM model endpoint
llm_model_type:
Choose the model type, supported: openai / ollama / claude / gemini
llm_model:
Choose the LLM model, currently supported:
openai: gpt-4o
ollama: llama2, mistral:v0.3
claude: any model
gemini: any model
llm_api_url:
Link of the API endpoint for the LLM model
openai: https://api.pawan.krd/cosmosrp/v1
ollama: http://127.0.0.1:11434/
claude: https://api.anthropic.com/v1
gemini: https://aistudio.google.com/app/apikey
Note: To run local Ollama, follow the guidelines here: Guide to Ollama deployment
3. plain_text_resume.yaml
This file contains your resume information in a structured format. Fill it out with your personal details, education, work experience, and skills. This information is used to auto-fill application forms and generate customized resumes.

Each section has specific fields to fill out:

personal_information:

This section contains basic personal details to identify yourself and provide contact information.
name: Your first name.
surname: Your last name or family name.
date_of_birth: Your birth date in the format DD/MM/YYYY.
country: The country where you currently reside.
city: The city where you currently live.
address: Your full address, including street and number.
zip_code: Your postal/ZIP code.
phone_prefix: The international dialing code for your phone number (e.g., +1 for the USA, +44 for the UK).
phone: Your phone number without the international prefix.
email: Your primary email address.
github: URL to your GitHub profile, if applicable.
linkedin: URL to your LinkedIn profile, if applicable.
Example
personal_information:
  name: "Jane"
  surname: "Doe"
  date_of_birth: "01/01/1990"
  country: "USA"
  city: "New York"
  address: "123 Main St"
  zip_code: "520123"
  phone_prefix: "+1"
  phone: "5551234567"
  email: "jane.doe@example.com"
  github: "https://github.com/janedoe"
  linkedin: "https://www.linkedin.com/in/janedoe/"
education_details:

This section outlines your academic background, including degrees earned and relevant coursework.

degree: The type of degree obtained (e.g., Bachelor's Degree, Master's Degree).
university: The name of the university or institution where you studied.
final_evaluation_grade: Your Grade Point Average or equivalent measure of academic performance.
start_date: The start year of your studies.
graduation_year: The year you graduated.
field_of_study: The major or focus area of your studies.
exam: A list of courses or subjects taken along with their respective grades.
Example:

education_details:
  - education_level: "Bachelor's Degree"
    institution: "University of Example"
    field_of_study: "Software Engineering"
    final_evaluation_grade: "4/4"
    start_date: "2021"
    year_of_completion: "2023"
    exam:
      Algorithms: "A"
      Data Structures: "B+"
      Database Systems: "A"
      Operating Systems: "A-"
      Web Development: "B"
experience_details:

This section details your work experience, including job roles, companies, and key responsibilities.

position: Your job title or role.
company: The name of the company or organization where you worked.
employment_period: The timeframe during which you were employed in the role, using the format MM/YYYY - MM/YYYY.
location: The city and country where the company is located.
industry: The industry or field in which the company operates.
key_responsibilities: A list of major responsibilities or duties you had in the role, e.g. responsibility: "Developed web applications using React and Node.js".
skills_acquired: Skills or expertise gained through this role, e.g. "React".
Example:

experience_details:
  - position: "Software Developer"
    company: "Tech Innovations Inc."
    employment_period: "06/2021 - Present"
    location: "San Francisco, CA"
    industry: "Technology"
    key_responsibilities:
      - responsibility: "Developed web applications using React and Node.js"
      - responsibility: "Collaborated with cross-functional teams to design and implement new features"
      - responsibility: "Troubleshot and resolved complex software issues"
    skills_acquired:
      - "React"
      - "Node.js"
      - "Software Troubleshooting"
projects:

Include notable projects you have worked on, including personal or professional projects.

name: The name or title of the project.
description: A brief summary of what the project involves or its purpose.
link: URL to the project, if available (e.g., GitHub repository, website).
Example:

projects:
  - name: "Weather App"
    description: "A web application that provides real-time weather information using a third-party API."
    link: "https://github.com/janedoe/weather-app"
  - name: "Task Manager"
    description: "A task management tool with features for tracking and prioritizing tasks."
    link: "https://github.com/janedoe/task-manager"
achievements:

Highlight notable accomplishments or awards you have received.

name: The title or name of the achievement.
description: A brief explanation of the achievement and its significance.
Example:

achievements:
  - name: "Employee of the Month"
    description: "Recognized for exceptional performance and contributions to the team."
  - name: "Hackathon Winner"
    description: "Won first place in a national hackathon competition."
certifications:

Include any professional certifications you have earned.

name: "PMP"
description: "Certification for project management professionals, issued by the Project Management Institute (PMI)"
Example:

certifications:
  - "Certified Scrum Master"
  - "AWS Certified Solutions Architect"
languages:

Detail the languages you speak and your proficiency level in each.

language: The name of the language.
proficiency: Your level of proficiency (e.g., Native, Fluent, Intermediate).
Example:

languages:
  - language: "English"
    proficiency: "Fluent"
  - language: "Spanish"
    proficiency: "Intermediate"
interests:

Mention your professional or personal interests that may be relevant to your career.

interest: A list of interests or hobbies.
Example:

interests:
  - "Machine Learning"
  - "Cybersecurity"
  - "Open Source Projects"
  - "Digital Marketing"
  - "Entrepreneurship"
availability:

State your current availability or notice period.

notice_period: The amount of time required before you can start a new role (e.g., "2 weeks", "1 month").
Example:

availability:
  notice_period: "2 weeks"
salary_expectations:

Provide your expected salary range.

salary_range_usd: The salary range you are expecting, expressed in USD.
Example:

salary_expectations:
  salary_range_usd: "80000 - 100000"
self_identification:

Provide information related to personal identity, including gender and pronouns.

gender: Your gender identity.
pronouns: The pronouns you use (e.g., He/Him, She/Her, They/Them).
veteran: Your status as a veteran (e.g., Yes, No).
disability: Whether you have a disability (e.g., Yes, No).
ethnicity: Your ethnicity.
Example:

self_identification:
  gender: "Female"
  pronouns: "She/Her"
  veteran: "No"
  disability: "No"
  ethnicity: "Asian"
legal_authorization:

Indicate your legal ability to work in various locations.

eu_work_authorization: Whether you are authorized to work in the European Union (Yes/No).
us_work_authorization: Whether you are authorized to work in the United States (Yes/No).
requires_us_visa: Whether you require a visa to work in the United States (Yes/No).
requires_us_sponsorship: Whether you require sponsorship to work in the United States (Yes/No).
requires_eu_visa: Whether you require a visa to work in the European Union (Yes/No).
legally_allowed_to_work_in_eu: Whether you are legally allowed to work in the European Union (Yes/No).
legally_allowed_to_work_in_us: Whether you are legally allowed to work in the United States (Yes/No).
requires_eu_sponsorship: Whether you require sponsorship to work in the European Union (Yes/No).
canada_work_authorization: Whether you are authorized to work in Canada (Yes/No).
requires_canada_visa: Whether you require a visa to work in Canada (Yes/No).
legally_allowed_to_work_in_canada: Whether you are legally allowed to work in Canada (Yes/No).
requires_canada_sponsorship: Whether you require sponsorship to work in Canada (Yes/No).
uk_work_authorization: Whether you are authorized to work in the United Kingdom (Yes/No).
requires_uk_visa: Whether you require a visa to work in the United Kingdom (Yes/No).
legally_allowed_to_work_in_uk: Whether you are legally allowed to work in the United Kingdom (Yes/No).
requires_uk_sponsorship: Whether you require sponsorship to work in the United Kingdom (Yes/No).
Example:

legal_authorization:
eu_work_authorization: "Yes"
us_work_authorization: "Yes"
requires_us_visa: "No"
requires_us_sponsorship: "Yes"
requires_eu_visa: "No"
legally_allowed_to_work_in_eu: "Yes"
legally_allowed_to_work_in_us: "Yes"
requires_eu_sponsorship: "No"
canada_work_authorization: "Yes"
requires_canada_visa: "No"
legally_allowed_to_work_in_canada: "Yes"
requires_canada_sponsorship: "No"
uk_work_authorization: "Yes"
requires_uk_visa: "No"
legally_allowed_to_work_in_uk: "Yes"
requires_uk_sponsorship: "No"
work_preferences:

Specify your preferences for work arrangements and conditions.

remote_work: Whether you are open to remote work (Yes/No).
in_person_work: Whether you are open to in-person work (Yes/No).
open_to_relocation: Whether you are willing to relocate for a job (Yes/No).
willing_to_complete_assessments: Whether you are willing to complete job assessments (Yes/No).
willing_to_undergo_drug_tests: Whether you are willing to undergo drug testing (Yes/No).
willing_to_undergo_background_checks: Whether you are willing to undergo background checks (Yes/No).
Example:

work_preferences:
  remote_work: "Yes"
  in_person_work: "No"
  open_to_relocation: "Yes"
  willing_to_complete_assessments: "Yes"
  willing_to_undergo_drug_tests: "No"
  willing_to_undergo_background_checks: "Yes"
PLUS. data_folder_example
The data_folder_example folder contains a working example of how the files necessary for the bot's operation should be structured and filled out. This folder serves as a practical reference to help you correctly set up your work environment for the job search bot.

Contents
Inside this folder, you'll find example versions of the key files:

secrets.yaml
config.yaml
plain_text_resume.yaml
These files are already populated with fictitious but realistic data. They show you the correct format and type of information to enter in each file.

Using the data_folder_example
Using this folder as a guide can be particularly helpful for:

Understanding the correct structure of each configuration file
Seeing examples of valid data for each field
Having a reference point while filling out your personal files
Usage
Account language To ensure the bot works, your account language must be set to English.

Data Folder: Ensure that your data_folder contains the following files:

secrets.yaml
config.yaml
plain_text_resume.yaml
Output Folder: Contains the output of the bot.

data.json results of the --collect mode
failed.json failed applications
open_ai_calls.json all the calls made to the LLM model
skipped.json applications that were skipped
success.json successful applications
Note: answers.json is not part of the output folder and can be found in the root of the project. It is used to store the answers of the questions asked to the user. Can be used to update the bot with corrected answers. Search for Select an option, 0, Authorized, and how many years of to verify correct answers.

Run the Bot:

Auto_Jobs_Applier_AIHawk offers flexibility in how it handles your pdf resume:

Dynamic Resume Generation: If you don't use the --resume option, the bot will automatically generate a unique resume for each application. This feature uses the information from your plain_text_resume.yaml file and tailors it to each specific job application, potentially increasing your chances of success by customizing your resume for each position.

python main.py
Using a Specific Resume: If you want to use a specific PDF resume for all applications, place your resume PDF in the data_folder directory and run the bot with the --resume option:

python main.py --resume /path/to/your/resume.pdf
Using the colled mode: If you want to collect job data only to perform any type of data analytics you can use the bot with the --collect option. This will store in output/data.json file all data found from linkedin jobs offers.

python main.py --collect
