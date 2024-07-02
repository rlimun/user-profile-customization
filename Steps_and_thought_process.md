## Summary: 
This would be the steps and my thought process when working on test plans and automated test creation for new features. I worked in an Agile environment so my steps convey Agile methodologies and processes.

### Agile Test Plan and Automated Test Creation Process
**Steps:**
1. **Get Clarification on the Design Document:**
   - Collaborate with stakeholders to understand the design document thoroughly. Ensure all questions are answered before proceeding.
   - Agile Principle: Emphasizes collaboration and communication with stakeholders.

2. **Create a Test Plan Based on the Design Document:**
   - Develop a test plan that outlines the scope, objectives, and strategies based on the design document.
   - Agile Principle: Focus on clear, iterative planning.

3. **Create Test Scenarios for the Test Plan:**
   - Design test scenarios that will be stored in TestRail. Track which test cases are automated and which are not.
   - Agile Principle: Continuous integration and visibility of work progress.

4. **Update the Test Plan as We Go Along:**
   - Continuously refine and update the test plan as new information is discovered and questions are clarified.
   - Agile Principle: Embracing change and iterative improvement.

5. **Submit Test Plan for Sign-off:**
   - Present the test plan to all stakeholders for review and approval.
   - Agile Principle: Regular stakeholder involvement and feedback.

6. **Create Test Cases and Add Them to TestRail:**
   - Develop detailed test cases and enter them into TestRail for tracking.
   - Agile Principle: Documentation and traceability of requirements and tests.

7. **Create JIRA Tickets for Automated Test Creation:**
   - Generate JIRA tickets to track the creation of automated tests, linking them to the TestRail test cases.
   - Agile Principle: Task management and transparency.

8. **Automated Test Development:**
   - **When QAs Owned the Tests:** 
     - QAs pick up the JIRA tickets to work on automated tests when the first iteration of the feature is deployed (kept behind a proctor test at 0%).
   - **When SWEs Owned the Tests:**
     - SWEs develop the feature and work on the automated test coverage simultaneously.
   - Agile Principle: Cross-functional teams and collective ownership.

9. **Continuous Feedback and Updates:**
   - After the first deployment, gather ongoing feedback from stakeholders to refine and update the feature and its tests.
   - Agile Principle: Continuous improvement and iterative development.

10. **Bug Bash Meeting:**
    - Organize a bug bash where team members manually test the new feature.
    - Agile Principle: Collaborative testing and quality assurance.

11. **Incorporate Bug Bash Feedback:**
    - Collect feedback from the bug bash and make necessary changes.
    - Agile Principle: Adaptability and responsiveness to change.

12. **Feature Rollout:**
    - Once ready, turn on the proctor test and roll out the feature for all users.
    - Agile Principle: Incremental delivery and deployment.


### Thought process while creating the test plan:
I want to create the test plan but since the design doc has a lot of missing information, I would ask questions before creating my test plan, and they would be the following:

##### Questions regarding tools and technologies used:
- What tools, frameworks, and libraries will be used to create this feature?
   - Answer: The feature will be developed using React for the frontend, Node.js for the backend, and MongoDB for the database. The file upload functionality will be handled using the Multer library.
- It seems as if we are using a profile, so in order to grab profile data, what database are we grabbing from?
   - Answer: Profile data will be stored and retrieved from MongoDB.
- How is this data stored and retrieved from the database?
   - Answer: Profile data, including the profile picture URL, bio, and theme color, will be stored in MongoDB collections. Data is retrieved using RESTful API endpoints.
- Are there any new endpoints we are using and/or creating for this feature?
   - Answer: Yes, new endpoints will include:
      - POST /api/profile/picture for uploading profile pictures
      - DELETE /api/profile/picture for removing profile pictures
      - PUT /api/profile/bio for updating the bio
      - PUT /api/profile/theme for selecting a theme color
- Are there any specific environment configurations required for testing?
   - Answer: The testing environment for our automation coverage requires a mock MongoDB instance and mock endpoints for file uploads. Additionally, testing configurations need to include a tool for simulating network latency. When manually testing, we will use the real MongoDB instance and the real endpoints.

##### Questions regarding the actual feature:
- What would the error message look like if a user tried to:
   - Upload a file that's not of an accepted format
      - Answer: "Invalid file format. Please upload a JPEG, PNG, or GIF file."
   - Upload a file larger than 5mb
      - Answer: "File size exceeds the 5MB limit. Please upload a smaller file."
   - Add a bio larger tha maximum length
      - Answer: "Bio exceeds the maximum length of 250 characters. Please shorten your bio."
   - Remove a profile picture when there isn't any yet? Does the Remove button only appear when there is a profile picture?
      - Answer: "No profile picture to remove." The Remove button only appears when a profile picture is present.
- How many colors are there to choose from? What are they?
   - Answer: There are 8 colors to choose from: Red, Blue, Green, Yellow, Purple, Orange, Pink, and Teal.
- What kind of characters can be used in the bio?
   - Answer: The bio can include plain text only. Special characters such as emojis and symbols are allowed, but HTML and script tags are not.
- Are there any dependencies or third-party services involved in profile picture scanning or theme color application?
   - Answer: Yes, profile pictures will be scanned for viruses using the Cloudinary service. No third-party service is required for theme color application.
- What happens if upload process takes longer than expected?
   - Answer: If the upload process exceeds 5 seconds, a loading spinner will appear, and a message will inform the user that the upload is taking longer than usual. If it exceeds 30 seconds, an error message will prompt the user to try again.
- Are there any loading indicators or messages shown to the user during the upload or theme color selection process?
   - Answer: Yes, a loading spinner appears during the profile picture upload and theme color selection processes. Additionally, a "Saving changes..." message is displayed until the process is complete.

##### Other Questions:
- What is the goal of enhancing user engagement and how will this be measured?
   - Answer: The goal is to increase user engagement by 20% over the next six months. This will be measured using metrics such as the number of profile customizations, user activity on the profile page, and user feedback surveys.
- How will performance be monitored?
   - Answer: Performance will be monitored using application performance management (APM) tools like New Relic. Metrics will include profile picture upload time, theme color application time, and overall page load times.
- How accessible is this new feature? 
   - Answer: The feature will adhere to WCAG 2.1 AA standards. This includes screen reader compatibility, keyboard navigation support, and sufficient color contrast.
- Are there color contrast requirements for the theme color selection to ensure readability?
   - Answer: Yes, all theme colors will be tested to ensure they meet the minimum contrast ratio of 4.5:1 against the text and other UI elements for readability.

So in order to get my questions answered, I would go to Product Manager, UX Designer, SWE, Data Scientist, and/or whoever else and ask them corresponding questions. For the design doc, we usually used Google Docs and so I would usually just add a comment to the part of the page I needed an answer to and tag the person I would ask the question to. If there isn't a part in the doc where I could attach a comment to, we had a space at the bottom of the Design Doc with Questions so I would put my question there and then tag the person I would ask the question to.

Let's just say for this example that I went to the right people and got the following questions answered. I would make sure to add the answers to the questions in the doc. You could see those answers (used ChatGPT for this exercise) next to the questions above.

Once I have my questions answered, then I would be able to create a test plan that outlines the scope, objectives, and strategies based on the design document.

### Creating Test plan thoughts and clarification
#### Test Strategy 
When creating test plans, I would be the one to add the integration and end-to-end tests. Unit tests aren't usually added to the test plan because they are usually added as SWEs write the code, but in this case, I'll just add what components the unit tests should be written for. If you want to see what kind of unit tests I would write, please take a look at my other repo: project_flashcards.

#### Test case format:
| Test_case_id | Test_case_description | Desktop/Mobile | Priority | TestRail Link |

#### Risk Management
For Risk Management portion, I would write down some risks that I could think of or that other people have mentioned and during sign off and sharing of the test plan, others would chime in and say that this isn't a risk or this could be a risk and have suggestions for how to migitate the risk.

#### Personal Notes
It is very difficult to write a test plan for a feature where there are no mockups/design for, but I did my best during this exercise!

