# User Profile Test Plan

- Product Owner: Nezuko Kamado
- Engineers: Richelle Limun, Levi Ackerman 
- QA: Richelle Limun
- Designer: Satoru Gojo

## Important Links:
- [User Profile Design Doc](https://docs.google.com/document/d/162-3462_R-0t79072-800/edit?usp=sharing)
- Link to JIRA ticket of new feature
- Link to GitHub repository
- Link to Figma Design (or whatever tool we use to show the mockups and designs)

## Objectives
Purpose: The purpose of this test plan is to outline the strategy, resources, and approach to testing the user profile customization feature.
Goals: 
- Verify functional requirements
- Verify non-functional requirements such as performance and accessibility.
- Verify all P0 and P1 test scenarios have automation coverage before feature rollout (If there are P2 and P3, these can be worked on at a later date)
- Identify and log defects early in the development cycle.
- Support regression testing to ensure new changes do not impact existing functionality
- Ensure compliance with accessibility standards (WCAG 2.1 AA) and there is automated tests coverage for accessibility
- Facilitate user acceptance testing (UAT) with detailed test cases
- Provide clear reporting and metrics on testing progress and defect status

## Test Items
- Features to be Tested:
   - Profile Picture Upload
   - Bio Section
   - Theme Color Selection
   - User Interface (Profile Settings Page and Profile Page)
- Features not to be Tested:
   - Third-party service integrations

## Test Environment
- To be tested on: Desktop web browsers, mobile web browser, and mobile apps
- Databases: MongoDB
- Browsers: Chrome, Safari, Firefox
- Test Data: Sample user profiles, profile pictures
- Tools: TestRail, JIRA, Cypress, React Testing Library, Jest
- Automated tests will run on a mock instance of DB and we will mock the endpoints. We will manually test the feature in QA environment and also in Production environment.

## Testing Strategy
- Unit tests
   - Profile Picture Upload component
   - Bio section component
   - Theme color selection component
- Integration and End-to-end Automated tests
   - Profile Upload
      - | 001 | Verify that you could upload a profile picture within 5mb | Desktop | P0 | Link-to-TestRail |
         - Steps: Click to upload, mock `POST /api/profile/picture` endpoint and call it, verify that the profile picture is updated in the mock database, and verify that new profile picture appears in profile. Refresh the page and verify profile picture still appears
      - | 002 | Verify that you could upload a profile picture within 5mb | Mobile | P0 | Link-to-TestRail |
         - Steps: Click to upload, mock `POST /api/profile/picture` endpoint and call it, verify that the profile picture is updated in the mock database, and verify that new profile picture appears in profile. Refresh the page and verify profile picture still appears
      - | 003 | Verify that you cannot upload an unsupported file format and error message appears. | Desktop | P1 | Link-to-TestRail |
         - Steps: Click to upload, mock `POST /api/profile/picture` endpoint and call it, verify that the profile picture is not updated in the mock database, and verify that error message appears.
      - | 004 | Verify that you cannot upload an unsupported file format and error message appears. | Mobile | P1 | Link-to-TestRail |
         - Steps: Click to upload, mock `POST /api/profile/picture` endpoint and call it, verify that the profile picture is not updated in the mock database, and verify that error message appears.
      - | 005 | Verify that you cannot upload a profile picture larger than 5mb and error message appears. | Desktop | P1 | Link-to-TestRail |
         - Steps: Click to upload, mock `POST /api/profile/picture` endpoint and call it, verify that the profile picture is not updated in the mock database, and verify that error message appears.
      - | 006 | Verify that you cannot upload a profile picture larger than 5mb and error message appears. | Mobile | P1 | Link-to-TestRail |
         - Steps: Click to upload, mock `POST /api/profile/picture` endpoint and call it, verify that the profile picture is not updated in the mock database, and verify that error message appears.
      - | 007 | Verify that you can remove a profile picture | Desktop | P1 | Link-to-TestRail |
         - Steps: Click to remove, mock `DELETE /api/profile/picture` endpoint and call it, verify that the profile picture is removed from the mock database, and verify that the profile picture is removed from the profile. Refresh the page and verify profile picture is removed.
      - | 008 | Verify that you can remove a profile picture | Mobile | P1 | Link-to-TestRail |
         - Steps: Click to remove, mock `DELETE /api/profile/picture` endpoint and call it, verify that the profile picture is removed from the mock database, and verify that the profile picture is removed from the profile. Refresh the page and verify profile picture is removed.
   - Bio Section
      - | 009 | Verify that you can add a bio within 250 characters | Desktop | P0 | Link-to-TestRail |
         - Steps: Enter bio less than 250 characters, mock `POST /api/profile/bio` endpoint and call it, verify that the bio is updated in the mock database, and verify that new bio appears in profile, refresh the page and verify bio still appears
      - | 010 | Verify that you can add a bio within 250 characters | Mobile | P0 | Link-to-TestRail |
         - Steps: Enter bio less than 250 characters, mock `POST /api/profile/bio` endpoint and call it, verify that the bio is updated in the mock database, and verify that new bio appears in profile, refresh the page and verify bio still appears
      - | 011 | Verify that you cannot add a bio more than 250 characters and error message appears | Desktop | P1 | Link-to-TestRail |
         - Steps: Enter more than 250 characters in the bio and mock `POST /api/profile/bio` endpoint and call it, verify that the bio is not updated in the mock database, and verify that error message appears
      - | 012 | Verify that you cannot add a bio more than 250 characters and error message appears | Mobile | P1 | Link-to-TestRail |
         - Steps: Enter more than 250 characters in the bio and mock `POST /api/profile/bio` endpoint and call it, verify that the bio is not updated in the mock database, and verify that error message appears
      - | 013 | Verify character counter shows correct number of characters remaining | Desktop | P1 | Link-to-TestRail |
         - Steps: Enter 100 characters, verify character counter shows 150 characters remaining. Delete 50 characters and verify that the character counter shows 200 characters remaining.
      - | 014 | Verify invalid characters in bio gives an error message | Desktop | P1 | Link-to-TestRail |
         - Steps: Enter a script tag in the bio and verify that an error message appears
      - | 015 | Verify invalid characters in bio gives an error message | Mobile | P1 | Link-to-TestRail |
         - Steps: Enter a script tag in the bio and verify that an error message appears
   - Theme color selection
      - | 016 | Verify you can select a theme color and it changes | Desktop | P0 | Link-to-TestRail |
         - Steps: Select a color, click save, mock `PUT /api/profile/theme`, verify that the color is saved in the mock database, and verify that the color is applied to the profile
      - | 017 | Verify you can select a theme color and it changes | Mobile | P0 | Link-to-TestRail |
         - Steps: Select a color, click save, mock `PUT /api/profile/theme`, verify that the color is saved in the mock database, and verify that the color is applied to the profile
- Accessibility
   - Integrate axe devtools API into Cypress tests, we will run axe on each component and page for Desktop and Mobile, and make sure there are no violations. Axe checks for color contrast and other WCAG guidelines.
   - Run axe devtools in the web browser manually and check for violations
   - Check tabbing order of each component (Profile picture upload, bio section, theme color)
- Acceptance (We can test manually during the bug bash or when feature is in a pre-release state)
   - Profile Picture Upload:
      - Scenario 1: Upload Profile Picture
        - Steps:
            1. Log into the application.
            2. Navigate to the Profile Settings page.
            3. Upload a profile picture within the specified size limit (5 MB).
            4. Save the profile picture.
        - Expected Outcome:
            - Verify that the uploaded profile picture is displayed correctly on the user’s profile page.
            - Ensure the profile picture quality is clear and properly aligned.
   - Bio Section:
      - Scenario 2: Add Bio
         - Steps:
            1. Navigate to the Profile Settings page.
            2. Enter a bio within the maximum character limit (250 characters).
            3. Save the bio.
        - Expected Outcome:
            - Verify that the entered bio appears correctly on the user’s profile page.
            - Ensure the character counter updates accurately as text is entered.
   - Theme Color Selection:
      - Scenario 3: Select Theme Color
         - Steps:
           1. Navigate to the Profile Settings page.
           2. Select a theme color from the provided palette.
           3. Save the selected theme color.
      - Expected Outcome:
         - Verify that the selected theme color is applied consistently across the user’s profile page.
         - Check that the theme color persists after logging out and logging back in.
   - User Interface (UI) Testing:
      - Scenario 4: UI Consistency
         - Steps:
            1. Navigate through different pages of the user profile.
            2. Check the layout, responsiveness, and visual consistency of profile customization elements.
         - Expected Outcome:
            - Ensure that UI elements (buttons, inputs, colors) align with design specifications and are intuitive to use.

## Risk Management
   - Performance degradation after profile upload - could lead to a site slowdown or a slow performance of uploading a profile picture, which could lead to user not liking the feature
   - Security vulnerabilities in profile upload - could lead to a user profile's data being altered
   - Database corruption after profile upload - could lead to data loss or a user profile's data being altered
   - Compatibility issues across devices - data could end up not staying consistent across devices, i.e. User profile picture might not be displayed correctly on mobile or it might only be displayed on Desktop when it should be shown on both
   - User adoption issues - users could end up not liking this feature and this might fail to enhance user engagement

## Questions?

## Sign off


