# AutoRecruit

## Workflow Objective

The main goals of this workflow are:
1. Automated Resume Intake from form submissions.
2. Information Extraction from submitted resumes (PDF).
3. Resume Scoring based on predefined weighted criteria.
4. Candidate Filtering based on score.
5. Interview Scheduling with calendar integration.
6. Dynamic Question Generation using AI, tailored to resume and job description.

## Workflow Breakdown

1.Form Submission Trigger

This node is activated whenever a job application form is submitted by a candidate. The form submission includes a resume file, typically in PDF format, which is passed on to the next node for processing.


2. Extract from File (PDF)

The Extract from File node receives the uploaded resume and parses its contents. It extracts raw textual data from the PDF, preparing it for further semantic analysis.


3. Information Extractor (with Google Gemini Chat Model)

Once the raw resume text is extracted, it is passed into the Information Extractor node. This node uses the Google Gemini Chat Model to process the text and identify key candidate details such as the candidate's full name, email address, phone number, LinkedIn profile, educational qualifications, technical and soft skills, and professional work experience. This transforms an unstructured resume into a usable data format for further automation.


4. Company Detail

It contains important information such as the job description, preferred skills, experience expectations, and the company’s domain focus. This data is later used to assess the relevance of each candidate’s profile.


5. Filter Candidates (Scoring via LLM)

The Filter Candidates node is where the actual resume scoring takes place. It sends both the candidate information and the company/job data to another instance of the Google Gemini Chat Model.
It outputs a final score out of 100 along with feedback or reasoning that justifies the score.

6. IF Node: Score Threshold

The IF node evaluates whether the score meets a certain threshold. If the score is above the threshold, the candidate is shortlisted and the workflow proceeds to the interview scheduling process.


7. Convert to CSV + Remove Contact

The result of the filtering step, flows into the Convert to CSV node. This node formats the structured candidate data into CSV format for documentation and future analysis. It is followed by the Remove Contact node, which serves as a manual filtering step, allowing HR teams to remove duplicates or disqualified candidates if necessary before proceeding.

8.Schedule Interview Path (if passed)

For shortlisted candidates, the interview scheduling process begins by checking the interviewer’s availability using the Find Slot function and Google Calendar. Once available slots are identified, a suitable time is selected via the Propose Time function and booked using the Create Event node. Finally, the Process function handles post-scheduling tasks like sending confirmation emails and updating records.


9.Merge Node

In parallel, the Merge node aggregates both the resume information and the company’s job description. This combined data is then passed to the Question Generator node, which uses another Google Gemini Chat Model to generate personalized interview questions. These questions are tailored based on the candidate’s experience and the specific job requirements, and can include technical, behavioral, and project-based questions designed to evaluate the candidate thoroughly.

## Benefits of This Workflow

1. Fully Automated recruitment workflow, from intake to interview.
2. AI-Powered Resume Scoring ensures objectivity.
3. Dynamic Interview Questions boost relevance and personalization.
4. TimeSaving for recruiters and HR managers.
5. Scalable & Modular – suitable for companies hiring in volume.
